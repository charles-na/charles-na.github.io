---
layout: post
title: "ARKit by Example - Part1: AR Cube"
description: "첫 번째 포스트는 ARKit을 사용한 정말 간단한 hello world AR 앱을 만들 것입니다."
tags: [arkit,apple]
categories: [arkit]
---

첫 번째 예제는 ARKit을 사용한 정말 간단한 hello world AR 앱을 만들 것입니다. AR 월드에 3D 큐브를 배치하고, iOS 기기로 3D 큐브를 둘러 볼 수 있게 됩니다. 

ARKit에서 3D 컨텐츠를 렌더링하기 위해 SceneKit을 사용합니다. 이것은 iOS 장치에서 3D 그래픽을 렌더링하기 위한 프레임워크 입니다.

다음은 실제 앱의 동영상 입니다. ARKit을 사용하여 볼 수 있듯이 현실 세계에 가상 물체를 배치하고, 카메라를 움직일 때 가상 물체를 고정시킬 수 있습니다.

{::nomarkdown}
<iframe width="560" height="315" src="https://www.youtube.com/embed/cHuitQ0WAX0" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>
{:/nomarkdown}

 이것은 매우 간단한 응용 프로그램이지만 지오메트리 탐지, 3D 물리 및 훨씬 더 재미있는 것들을 포함하여 이러한 일련의 기사를 통해 점점 더 많은 기능을 구축 할 것입니다.


## Requirements

ARKit을 지원하기 위해서는 A9/A10 프로세서가 있는 iOS 장치가 있어야 합니다. 즉, iPhone 6S 이상 또는 iPad 2017 이상이어야 합니다.

### Creating the project

<figure>
	<a href="https://cdn-images-1.medium.com/max/1600/1*4d-Qovl_HSLbeEEB1MDEdg.png"><img src="https://cdn-images-1.medium.com/max/1600/1*4d-Qovl_HSLbeEEB1MDEdg.png" alt=""></a>
	<figcaption><a href="https://cdn-images-1.medium.com/max/1600/1*4d-Qovl_HSLbeEEB1MDEdg.png" title="image_title">Xcode를 열고, ARKit 프로젝트 템플릿을 선택하십시오.</a>.</figcaption>
</figure>

