#Jack&Jill에서 Retrolambda로 변경 해보기
- Jack Compiler가 나오면서, 새 프로젝트는 전부 다 사용해왔는데 날이 갈 수록 점점 한계치에 부딪히다보니 결국 다시 Retrolambda로 바꿔버렸다.

##기존
```gradle
    defaultConfig {
    ...
        jackOptions {
            enabled true
        }
    }
    
    }
    compileOptions {
        sourceCompatibility JavaVersion.VERSION_1_8
        targetCompatibility JavaVersion.VERSION_1_8
    }
```
##변경 후
```gradle
buildscript {
    repositories {
        ...
        mavenCentral()
    }
    dependencies {
        ...
        classpath 'me.tatarka:gradle-retrolambda:3.2.5'
    }
}


apply plugin: 'me.tatarka.retrolambda'

    defaultConfig {
    ...
        jackOptions {
            enabled false
        }
    }
    
    }
    compileOptions {
        sourceCompatibility JavaVersion.VERSION_1_8
        targetCompatibility JavaVersion.VERSION_1_8
    }
```

정말 어렵지 않게 변경할 수 있다.,   
어노테이션 때문에 오류가 생기지 않을까, 예상치 못한 오류가 무엇이 일을까, 생각하고 있었지만   
전혀 문제없이 빌드되어 디바이스에 동일한 앱이 정상적으로 작동하였다.