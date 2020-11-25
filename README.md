[![](https://jitpack.io/v/JobGetabu/NetworkX.svg)](https://jitpack.io/#JobGetabu/NetworkX)

# NetworkX
An easy & handy library to monitor device internet connection status 

## Features
* The real-time update on internet connection status changed
* Lightweight
* Provide both regular data or Live Data to observe from a fragment or an activity
* Thread Safe
* Cancel monitoring Internet connection status any time

## How does it work?
Once you start observing internet connection status by calling from your ``Application`` class `onCreate()`
method, ``NetworkX`` will start monitor internet connection status immediately under a `CoroutineScope` in a `IO Thread` 
for the thread safe purpose. ``NetworkX`` provide both traditional data which is `Boolean` or `MutableLiveData`
so that you can observe the status in a fragment or an activity.

---

### Library Preview

        https://www.youtube.com/watch?v=dHlhsvPF7RY
---

## Documentation

#### Installation
Step 1. Add the JitPack repository to your build file .

```gradle
    allprojects {
        repositories {
            maven { url 'https://jitpack.io' }
        }
    }
```

Step 2. Add the dependency.

```gradle
	dependencies {
	        implementation 'com.github.JobGetabu:NetworkX:Tag'
	}
```

---

### Version available

| Releases
| ------------- |
| 1.0           |
| 2.0.0           |

# Usages

##### Start observing internet connection status from your `Application` class.

To Start observing network status using ``NetworkX`` call `NetworkX.startObserving` from application `onCreate` method.
Otherwise, when try to check if device is connected to the internet or not it will throw an `Exception`
Provide `Application` reference & `NetworkXObservingStrategy` to `NetworkX` .

`NetworkXObservingStrategy` represent delay time in internet connection status checking
Sates are:


* NetworkXObservingStrategy.LOW
* NetworkXObservingStrategy.MEDIUM
* NetworkXObservingStrategy.HIGH
* NetworkXObservingStrategy.REALTIME


````
    override fun onCreate() {
        super.onCreate()
        NetworkX.startObserving(this, NetworkXObservingStrategy.HIGH)
    }
````
---

##### Also, you can provide custom time interval in millis.
Custom State:


* NetworkXObservingStrategy.CUSTOM
         
````
    override fun onCreate() {
        super.onCreate()
        NetworkX.startObserving(this, NetworkXObservingStrategy.CUSTOM(15 * 1000))
    }
````

---

##### How to check the connection status in a `Fragment` or an `Activity` or `Anywhere of the application` .

* To get status of internet connection for single time, use `NetworkX.isConnected` method to retrieve connection status

````
    NetworkX.isConnected().let {
        when (it) {
            true -> {
                /**
                 * Do your stuff here when internet is connected
                 */
                Log.d("NetworkX", "Is internet connected: $it")
            }
            else -> {
                /**
                 * Do your stuff here when internet is not connected
                 */
                Log.d("NetworkX", "Is internet connected: $it")
            }
        }
    }
````

or you can use extension function

````
    isInternetConnected().let {
        when (it) {
            true -> {
                /**
                 * Do your stuff here when internet is connected
                 */
                Log.d("NetworkX", "Is internet connected: $it")
            }
            else -> {
                /**
                 * Do your stuff here when internet is not connected
                 */
                Log.d("NetworkX", "Is internet connected: $it")
            }
        }
    }
````

---

* To get status of internet connection in realtime, use `NetworkX.isConnectedLiveData` method to retrieve connection status.

````
    NetworkX.isConnectedLiveData().observe(
        fragment/activity),
        Observer {
            when (it) {
                true -> {
                    /**
                     * Do your stuff here when internet is connected
                     */
                    Log.d("NetworkX", "Is internet connected: $it")
                }
                else -> {
                    /**
                     * Do your stuff here when internet is not connected
                     */
                    Log.d("NetworkX", "Is internet connected: $it")
                }
            }
        }
    )
````

or you can use extension function

````
    isInternetConnectedLiveData().observe(this, Observer {
        when (it) {
            true -> {
                /**
                 * Do your stuff here when internet is connected
                 */
                Log.d("NetworkX", "Is internet connected: $it")
            }
            else -> {
                /**
                 * Do your stuff here when internet is not connected
                 */
                Log.d("NetworkX", "Is internet connected: $it")
            }
        }
    })
````

---

* If you want to cancel the observing if internet is connected status, use `NetworkX.cancelObserving` method

````
    NetworkX.cancelObserving()

````

or you can use extension function

````
    cancelObservingIsInternetConnected()
````

---

### Contact me
[LinkedIn](https://www.linkedin.com/in/job-getabu/)

---

### License
[Apache Version 2.0](http://www.apache.org/licenses/LICENSE-2.0.html)


