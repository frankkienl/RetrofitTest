# RetrofitTest
Minimal test project to demonstrate build-problem
  
I've found a build-problem, that I have not been able to solve.  
(There is a workaround though)
  
The build-problem occurs when you try to build an app that uses the following libraries:
  
- Google Maps  
- Retrofit  
- okhttp3 idling resource (testing)  
- espresso (testing)  
  
![Image of build-prblem](https://raw.githubusercontent.com/frankkienl/RetrofitTest/master/Screen%20Shot%202017-09-21%20at%2009.58.30.png)
  
The workaround is to not test your app, and disable the libraries:  
- okhttp3 idling resource (testing)
- espresso (testing)
  
See:
[build.gradle](https://github.com/frankkienl/RetrofitTest/blob/master/app/build.gradle#L41)

```
dependencies {
    implementation fileTree(dir: 'libs', include: ['*.jar'])
    //Support
    implementation 'com.android.support:appcompat-v7:26.1.0'

    //RestClient
    implementation 'com.squareup.retrofit2:retrofit:2.2.0'
    implementation 'com.squareup.retrofit2:converter-gson:2.2.0'
    implementation 'com.squareup.okhttp3:logging-interceptor:3.7.0'

    //Google Maps
    implementation 'com.google.android.gms:play-services-maps:11.4.0'
    implementation 'com.google.maps.android:android-maps-utils:0.5'

    //Test
    testImplementation 'junit:junit:4.12'
    androidTestImplementation 'com.android.support.test:runner:1.0.1'
    androidTestImplementation 'com.android.support.test.espresso:espresso-core:3.0.1'
    //Make sure espresso waits for http-calls to end with idling-resource
    implementation 'com.jakewharton.espresso:okhttp3-idling-resource:1.0.0' //COMMENT TO BE ABLE TO BUILD
    implementation 'com.android.support.test.espresso:espresso-core:3.0.1'  //COMMENT TO BE ABLE TO BUILD
    androidTestImplementation('com.android.support.test.espresso:espresso-core:3.0.1', {
        exclude group: 'com.android.support', module: 'support-annotations'
    })
}
```
