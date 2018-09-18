# RxBindings

[RxCocoa](https://github.com/ReactiveX/RxSwift/tree/master/RxCocoa/iOS) can simplify connecting the UI fields with the View Model Input/Output. Furthermore, with the help of Swift extensions, this can save lots of time and code.


## Output
 An extensions from the View Model Output to the ViewController can be made and would look something like this:

```
fileprivate extension DetailsViewModelOutput {
    func bind(toViewController viewController: DetailsViewController) -> [Disposable] {
        return [
            //put your bindings here
        ]
    }
}

```
For example, assume a View is visible/gone depending on a View Model output stream:
```
details.drive(viewController.detailsLabel.rx.text),
```
Every time that the stream emits a new value, the text of the label will be changed.

## Input

The same applies for the Input: an extension is created accepting the ViewController as a parameter:
```

fileprivate extension DetailsViewModelInput {
    func bind(toViewController viewController: DetailsViewController) -> [Disposable] {
        return [
            //put your bindings here
        ]
    }
}
```
__Note:__ The code snippets shown below are placed within the upper code block, hence *this* refers to the ViewModelInput in this case.

This is the place to connect any Tap Listeners or Text Watchers. For example, let's assume we have a submit button that needs to communicate to the view model the intention of the user:

```
   viewController.reloadButton.rx.tap
                .startWith(())
                .bind { [weak self] in self?.fetch() }

```