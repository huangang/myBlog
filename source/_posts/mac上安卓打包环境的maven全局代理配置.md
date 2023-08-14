title: mac上安卓打包环境的maven全局代理配置
date: 2019-07-09 10:31:34
tags: [mac, android, maven]
---
> 国内maven太慢,用全局代理替换成阿里云的源
<!-- more -->
## 配置
路径:`~/.gradle/init.gradle`
``` gradle
allprojects{
    buildscript {
        repositories {
            def ALIYUN_REPOSITORY_URL = 'https://maven.aliyun.com/repository/google'
            def ALIYUN_JCENTER_URL = 'https://maven.aliyun.com/repository/jcenter'
            all { ArtifactRepository repo ->
                if(repo instanceof MavenArtifactRepository){
                    def url = repo.url.toString()
                    if (url.startsWith('https://repo1.maven.org/maven2')||url.startsWith('https://dl.google.com/dl/android/maven2')||url.startsWith('https://maven.google.com')) {
                        project.logger.lifecycle "Repository ${repo.url} replaced by $ALIYUN_REPOSITORY_URL."
                        remove repo
                    }
                    if (url.startsWith('https://jcenter.bintray.com/')) {
                        project.logger.lifecycle "Repository ${repo.url} replaced by $ALIYUN_JCENTER_URL."
                        remove repo
                    }
                }
            }
            maven {
            url ALIYUN_REPOSITORY_URL
        }
        maven{
            url ALIYUN_JCENTER_URL
        }
            }
    }
    repositories {
        def ALIYUN_REPOSITORY_URL = 'https://maven.aliyun.com/repository/google'
        def ALIYUN_JCENTER_URL = 'https://maven.aliyun.com/repository/jcenter'
        all { ArtifactRepository repo ->
            if(repo instanceof MavenArtifactRepository){
                def url = repo.url.toString()
                if (url.startsWith('https://repo1.maven.org/maven2')||url.startsWith('https://dl.google.com/dl/android/maven2')) {
                        project.logger.lifecycle "Repository ${repo.url} replaced by $ALIYUN_REPOSITORY_URL."
                        remove repo
                    }
                if (url.startsWith('https://jcenter.bintray.com/')) {
                    project.logger.lifecycle "Repository ${repo.url} replaced by $ALIYUN_JCENTER_URL."
                    remove repo
                }
            }
        }
        maven {
            url ALIYUN_REPOSITORY_URL
        }
        maven{
            url ALIYUN_JCENTER_URL
        }
    }
}
```
