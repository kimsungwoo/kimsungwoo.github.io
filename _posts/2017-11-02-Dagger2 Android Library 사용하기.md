---
layout: post
title: "Dagger2 Android Library 사용하기"
date: "2017-11-02"
slug: "example_content"
description: "Dagger2에서 Android용 Library가 별도로 나왔습니다.Support Library를 사용하신다면 'com.google.dagger:dagger-android-support:2.11'를 추가해주시면됩니다.필요하면 gradle은 annotationProcessor를 지원하는 버전으로 Upgrade"
category: 
  - 개발
  - 안드로이드
# tags will also be used as html meta keywords.
tags:
  - dagger
  - kotlin
  - android
show_meta: true
comments: true
mathjax: true
gistembed: true
published: true
noindex: false
nofollow: false
# hide QR code, permalink block while printing.
hide_printmsg: false
# show post summary or full post in RSS feed.
summaryfeed: false
## for twitter summary card with squared image and page description or page excerpt:
# imagesummary: foo.png
## for twitter card with large image:
# imagefeature: "http://img.youtube.com/vi/VEIrQUXm_hY/0.jpg"
## for twitter video card: (active for this page)
videofeature: ""
imagefeature: ""
videocredit: 
---


* TOC
{:toc}



#Dagger2






#Dagger2-Android


Dagger2에서 Android용 Library가 별도로 나왔습니다.

Support Library를 사용하신다면 'com.google.dagger:dagger-android-support:2.11'를 추가해주시면됩니다.
필요하면 gradle은 annotationProcessor를 지원하는 버전으로 Upgrade

{% highlight gradle %}
dependencies {
    compile 'com.google.dagger:dagger-android:2.11'
    compile 'com.google.dagger:dagger-android-support:2.11' // if you use the support libraries
    annotationProcessor 'com.google.dagger:dagger-android-processor:2.11'
    annotationProcessor 'com.google.dagger:dagger-compiler:2.11'
}
{% endhighlight %}





[Application]

class UILApplication : Application() , HasActivityInjector {
    @Inject lateinit var activityInjector: DispatchingAndroidInjector<Activity>

    override fun activityInjector(): AndroidInjector<Activity> {
        return activityInjector
    }

    override fun onCreate() {
        super.onCreate()
        DaggerAppComponent.builder()
                .application(this)
                .build()
                .inject(this)
    }
}

기존에 Application단에서 HasActivityInjector를 추가한후


[AppComponent]

@Singleton
@Component(modules = arrayOf(
        AndroidInjectionModule::class,
        AppModule::class,
        ActivitiesBuilder::class
))
interface AppComponent {
    @Component.Builder
    interface Builder {
        @BindsInstance
        fun application(application: Application): Builder
        fun build(): AppComponent
    }


    fun inject(app: UILApplication)
}
AppComponent 에서 3개의 Component를 주입해줍니다


[ActivitiesBuilder]

@Module
abstract class ActivitiesBuilder {

    @ContributesAndroidInjector(modules = arrayOf(SplashActivityModule::class))
    internal abstract fun bindMainActivity(): SplashActivity
}
Activity에 사용하는 모듈을 연결합니다.


[AppModule]
@Module
class AppModule {

    @Provides
    @Singleton
    fun provideContext(application: Application): Context {
        return application
    }


    @Provides
    @Singleton
    fun appExcuter(): AppExecutors{
        return AppExecutors()
    }

}
App에서 사용하는 공통 객체를 Provider!


[Activity]
open class BaseActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        AndroidInjection.inject(this)
        super.onCreate(savedInstanceState)
    }
}
전 Activity에서 Injection을 주입 후


해당 Activity에서 Inject후 사용



[Reference]
WIki : https://github.com/codepath/android_guides/wiki/Dependency-Injection-with-Dagger-2
