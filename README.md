# Bayes

Bayes is a [Naive Bayes Classifier](http://en.wikipedia.org/wiki/Naive_Bayes_classifier) for iOS and Mac platforms. 

Bayes is implemented in Swift, and takes advantage of generics to let you classify any type of your choosing.

## Installation

Bayes is available as a CocoaPod, but has not yet been versioned and submitted to trunk. So to use it:
```ruby
pod 'Bayes', git: 'https://github.com/fcanas/Bayes.git'
```

Since Bayes is written in Swift, you will need to be using a recent version of CocoaPods (>0.36) and you may need to add `use_frameworks!` to your Podfile. See [this blog post](http://blog.cocoapods.org/CocoaPods-0.36/) for more information.

## Use

```swift
var eventSpace = EventSpace<String, String>()

eventSpace.observe("Cat", features: ["paw", "tail", "claw"])
eventSpace.observe("Cat", features: ["stripe", "tail", "whisker", "ear"])
eventSpace.observe("Cat", features: ["meow", "vertical pupil"])

eventSpace.observe("Dog", features: ["paw", "tail", "bark"])
eventSpace.observe("Dog", features: ["wag", "fetch", "tail", "paw"])

var classifier = BayesianClassifier(eventSpace: eventSpace)

XCTAssertEqual(classifier.classify(["claw", "tail"])!, "Cat", "Should categorize as Cat, due to claw")
XCTAssertEqual(classifier.classify(["bark", "tail"])!, "Dog", "Should categorize as Dog, due to bark")
XCTAssertEqual(classifier.classify(["tail"])!, "Cat", "Should categorize as Cat, due to base rate")
XCTAssertEqual(classifier.classify(["paw", "tail"])!, "Dog", "Should categorize as Dog, due to prevalence of paw")
XCTAssertEqual(classifier.classify(["paw", "tail", "meow"])!, "Cat", "Should categorize as Cat, due to prevalence of paw")
```

## TODO

* Documentation
* Other Bayesian methods
* Continuous Integration
