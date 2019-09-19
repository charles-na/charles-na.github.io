---
layout: post
title: "FragmentPagerAdapter"
description: "FragmentPagerAdapter 메모리 누수 위험"
tags: [android, memory]
categories: [android]
---

## 기본적인 차이점
#### FragmentPagerAdapter
제한된(고정) 갯수의 항목(Fragment)인 경우 FragmentPagerAdapter가 적합하다. 왜냐하면 한 번 생성되면 Fragment의 인스턴스를 FragmentManager에서 절대로 제거하지 않기 때문이다.(Activity가 종료되지 않는 한).
#### FragmentStatePagerAdapter
메모리에 좀 더 요령이 있다. 범위 밖의 Fragment 인스턴스를 FragmentManager에서 완정히 제거한다. 제거된 Fragment의 상태는 FragmentStatePagerAdapter 내부에 저장된다. Fragment 인스턴스는 다시 돌아왔을 때 재생성되고 상태는 복원된다. 이 Adapter는 개수가 미정인 리스트나 항목이 자주 변경되는 리스트에 적합하다.
## FragmentPagerAdapter 메모리 누수 위험
FragmentPagerAdapter의 Fragment들은 detached만 되며, 절대로 FragmentManager에서 제거되지 않는다(Activity가 종료되지 않는한). FragmentPagerAdapter를 사용할 때는 반드시 onDestroyView() 에서 현재 View 또는 Context에 대한 참조를 제거해야 한다. 그렇지 않으면 가비지 콜렉터는 전체 View 또는 심지어 Activity를 릴리즈 할 수 없다. 이는 View/Context 관련 필드를 null로 설정하기(ButterKnife는 자동으로 바인드를 해제할 수 있다)와 Context 또는 View를 누수 시킬 수 있는 모든 리스너를 제거함을 의미한다.
#### detach된 좀비 fragment들
adapter에 묶인 작은 list의 항목들을 끊임없이 변경하면 메모리에 수백개의 detach된 인스턴스를 가질 수 있다. 이것은 새 항목을 만들고 오래된 detach된 Fragment들을 유지할 것이다. 
이는 FragmentStatePagerAdapter에서는 문제가 적다. 이것은 전체 Fragment 인스턴스들을 FragmentManager에서 제거하기ㄷ 때문이다. 많은 Fragment들을 스와이프하면 사고를 일으킬 수 있다. 각각의 것들이 새로운 Bundle 인스턴스 맵에 추가하기 때문에 상당히 커질 수 있다
(화면 회전 중에 TransactionTooLargeException을 일으킬 가능성이 있다.)
## notifyDataSetChanged()의 문제들
notifyDataSetChanged()는 데이터 세트가 변경되는 상황을 위한 것임에 주목하는 것이 중요하다. 이는 일부 항목들이 제거되거나 추가되었을 때를 의미한다. notifyDataSetChanged() 메소드는 현재 표시되고 있는 Fragment나 그들의 view들을 갱신하기 위한 용도가 아니다. 만약 일부 데이터가 변경되어 그들의 뷰들을 갱신하고자 한다면 당신의 Fragment에 Listener/Callback을 추가해야 한다.
## FragmentPagerAdapter & notifyDataSetChanged()
데이터 세트 변경을 지원하기 위해서 당신의 FragmentPagerAdapter에 두 메소드를 오버라이드해야 한다.
#### int getItemPosition(Obect object)
호스트 뷰가 항목의 위치가 변경되었는지를 판단하기 위해 호출 된다. 주어진 위치가 변경되지 않는 경우 POSITION_UNCHANGED를 반환하고 항목이 더 이상 존재하지 않는다면 POSITION_NONE을 반환한다.
이것의 기본 구현은 항목들이 위치를 절대로 변경하지 않을 것이라고 가정하고 항상 POSITION_UNCHANGED를 반환한다.
#### long getItemId(int position)
주어진 position에 있는 항목의 고유 식별자를 반환한다. 이것의 기본 구현은 주어진 위치를 반환한다. 항목들의 위치가 변경될 수 있다면 서브클래스는 이 메소드를 오버라이드 해야 한다.
