---
layout: post
title: "Retrofit 인스턴스 만들기zzz"
description: "Retrofit 인스턴스 만들기"
tags: [android, retrofit]
categories: [android]
---

## Retrofit 인스턴스 만들기
Retrofit을 사용하여 REST API에 네트워크 Request를 보내려면 Retrofit.Builder 클래스를 사용하여 인스턴스를 만들고, Base URL을 구성해야 합니다.
data 패키지 안에 remote라는 서브 패키지를 생성합니다. 이제 remote 패키지 내부에 RetrofitClient라는 이름의 Java 클래스를 생성합니다. 이 클래스는 Retrofit의 싱글톤을 생성합니다.
    
    import retrofit2.Retrofit;
    import retrofit2.converter.gson.GsonConverterFactory;

    public class RetrofitClient {
        private static Retrofit retrofit = null;
        public static Retrofit getClient(String baseUrl) {
            if (retrofit == null) {
                retrofit = new Retrofit.Builder()
                        .baseUrl(baseUrl)
                        .addConverterFactory(GsonConverterFactory.create())
                        .build();
            }
            return retrofit;
        }
    }
    
## API Interface 만들기
remote패키지 안에, SOService라는 이름의 Interface를 생성합니다. 이 Interface는 GET, POST, PUT, PATCH, DELETE와 같은 HTTP Request를 처리하는데 사용 할 메서드를 포함하고 있습니다.

    import retrofit2.Call;
    import retrofit2.http.GET;

    public interface SOService {
        @GET("/answers?order=desc&sort=activity&site=stackoverflow")
        Call<SOAnswersResponse> getAnswers();

        @GET("/answers?order=desc&sort=activity&site=stackoverflow")
        Call<SOAnswersResponse> getAnswers(@Query("tagged") String tags);
    }

#### 어노테이션 설명
* @Path	API 엔드포인트의 변수를 대채
* @Query	어노테이션의 매개변수 값으로 쿼리 키 이름을 지정
* @Body	Post 호출의 페이로드
* @Header	어노테이션의 매개변수 값으로 헤더를 지정

## API 유틸 만들기
이제 유틸리티 클래스를 생성합니다. ApiUtils 라는 이름입니다. 이 클래스는 statics 변수인 base URL 을 가지고 있고, getSOService() static 메소드를 통해 SOService 인터페이스를 어플리케이션에게 제공합니다.

    public class ApiUtils {
        public static final String BASE_URL = "https://api.stackexchange.com/2.2/";

        public static SOService getSOService() {
            return RetrofitClient.getClient(BASE_URL).create(SOService.class);
        }
    }
