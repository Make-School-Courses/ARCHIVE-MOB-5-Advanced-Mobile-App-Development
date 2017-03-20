# Distributing information in iOS

### Objectives

- What does information distribution mean?
- Delegation
- Closures
- Notifications
- Property Observers
- Bindings / Key Value Observation

## Information distribution

Mobile apps are highly interactive and multiple interfaces drive data changes: UI, Network etc
Main task is responding to events and distributing new data

## Code Locality

Each piece of code needs well defined responsibility. Eg. The code that triggers network request is not necessarily the code that is interested in response

## Type to type communication

Typically used to establish a life long connection

```swift
class UserViewController: UIViewController {

 func infoButtonTapped() {
 // communicate with business logic
 }

}

class UserView {

 weak var userViewController: UserViewController?

 func infoButtonTapped() {
    userViewController?.infoButtonTapped()
 }

}

```

**Tight coupling!**

The UserView could call any method provided by UserViewController,
including all the ones inherited from UIView Controller

UserView can become dependent on UIViewController.

UserView has to deal with huge interface:
```
func infoButtonTapped()
//…
init(nibName nibNameOrNil: String?, bundle nibBundleOrNil: NSBundle?)
var view: UIView!
func loadView()
var nibName: String? { get }
var nibBundle: NSBundle? { get }
var storyboard: UIStoryboard? { get }
//…
```

**Pros:**
    - Easy to use
**Cons:**
    - Results in tight coupling 
    - No tight interface for communication between two types
    - Mostly only useful for 1-1 communication
    
## Delegation
Typically used to establish a life long connection 

- Create a formal protocol that describes the
communication interface
- Use this protocol to create an indirect
connection between the two types

![Delegation](delegation.png)

Indirection = looser coupling

**Pros:**
    - Decouples communication, easy to replace delegate with
    any other type conforming to protocol 
    - Tight interface that contains only methods that are relevant
    for this specific communication channel 
    
**Cons:**
    - Mostly only useful for 1-1 communication

## Closures
Typically used for short lived relationships 

**Pros:**
    - Decouples communication
    - Provides a communication interface with only a single
    function
    
**Cons:**
    - Need to be careful to avoid retain cycles

## Notifications & NotificationCenter
Notifications allow us to broadcast information (1 to N) 
Sender has no information about which objects have subscribed to notifications

### Posting a notification
```swift
func synchronize() {
     // network request
     NSNotificationCenter.defaultCenter().postNotificationName("MyApp.SynchronizationCompleted", object: self)
 }
 
```

- Notifications are delivered on the same thread on which they are posted!
- Optionally you can use a userData argument to attach arbitrary data to the notification

### Registering for Notifications

```swift
class Listener {
    init() {
        NSNotificationCenter.defaultCenter().addObserver(self, selector: "syncComplete", name: nil, object: nil)
    }

    @objc func syncComplete() {
        // work
        print("ok")
    }
}
```

- Specify which notification you want to
listen to
- Specify which method on which object
should be called once this notification
occurs
- Mark the target method with @objc if you are not subclassing from an Objective-C object

#### Notification Gotchas

- Don’t forget to unsubscribe!

If a deallocated object is registered
with the notification center, your app
will crash on an attempt to deliver a
notification to the dead object

```swift
class Listener {

    deinit {
        NSNotificationCenter.defaultCenter().removeObserver(self)
    }
 //…
}

class UserViewController: UIViewController {

    override func viewDidDisappear(animated: Bool) {
        super.viewDidDisappear(animated)

        NSNotificationCenter.defaultCenter().removeObserver(self)
        }
}
```

- **Pros:**
    - Easy to communicate with different parts of the program without
    explicit references

- **Cons:**
    - No well defined communication interface / no type information
    - Causes crashes if you forget to unregister
    - Can create dependencies between code that should not be
    coupled


## Property Observers

Implicitly propagate changes within an instance of a type
Used for information propagation within an instance 

```swift
class UserViewController: UIViewController {
     var label: UILabel!

     var user: User? {
         didSet {
             if let label = label, let user = user {
                label.text = user.name
             }
         }
     }
 }
 ```
 
 - **Pros:**
    - Easy to use, type safe
    
- **Cons:**
    - Not applicable in many scenarios
    
    
## Bindings - Key-Value-Observation(KVO)

Objective-C API that relies on the Objective-C Runtime

Generates notifications when an observed property on
an observed object changes

Think: property observers for other objects

```swift
class Observer: NSObject {

    var user: User

    init(user: User) {
        self.user = user

        super.init()

        self.user.addObserver(self, forKeyPath: "name", options: NSKeyValueObservingOptions.New, context: nil)
    }
}

 override func observeValueForKeyPath(keyPath: String?, ofObject object: AnyObject?, change: [String : AnyObject]?, context:
UnsafeMutablePointer<Void>) {

    if let newValue = change?[NSKeyValueChangeNewKey] {
        print("Name changed: \(newValue)")
    } else {
        super.observeValueForKeyPath(keyPath, ofObject: object, change: change, context: context)
    }
    

    deinit {
        self.user.removeObserver(self, forKeyPath: "name")
    }
}
```

- **Pros:**
    - Allows observation of (almost) any property without additional work
    on class that is being observed 
    
- **Cons:**
    - API doesn’t provide type information of observed values 
    - API is arcane, e.g. one callback for all observer properties 
    - Not available on Swift classes, need to inherit from NSObject and
    use the dynamic keyword
    

Swift doesn’t have it’s own KVO mechanism, but there are third party alternatives and it’s easy to implement your own KVO alternative

Example frameworks include Bond, RxSwift, ReactiveCocoa

## Summary

- Delegation
- Closures
- Notifications
- Property Observers
- Bindings / Key Value Observation

## Resources
[NotificationCenter Apple](https://developer.apple.com/library/mac/documentation/Cocoa/Reference/Foundation/Classes/NSNotificationCenter_Class/)

[Swift Property Observers](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Properties.html#//apple_ref/doc/uid/TP40014097-CH14-ID262)

[NSHipster KVO](http://nshipster.com/key-value-observing/)

[RxSwift](https://github.com/ReactiveX/RxSwift)

[ReactiveCocoa](https://github.com/ReactiveCocoa/ReactiveCocoa)


# Next - [Networking Overview](../05-Networking-Overview/networking-overview.md)