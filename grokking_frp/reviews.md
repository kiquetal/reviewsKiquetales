# Reactive Functional Programming
## Capitulo I

Benefits of FRP
... Testability with unit Test
... Revealed obscure issues
... Handling of asynchronus operations

Tips:The subscriber does not know where and when the data comes from., or how many pieces of it.

Debounce:only emit an item from Observable. If a particular timespan has passed without it emitting another item.

RxTextView.textChanges(textInput)
.filter(text->text.length()>3)
.debounce(150,TimeUnit.MILLISECONDS)
.subscribe(this::updateSearchResults);

Requierements:
-Run after UI is created.
-Run only once for the created UI

AndroidSchedulers.mainThread()

Terminology:
- downstream
- upstream

Exercise I:
Make an EditText and a TextView have the textView says "Text too long" after user has typed more than 7 characters.

Libraries on Android:
-Retrofit
dependencies{


  com.squareup.retrofit2:retrofit:2.0.0-beta4
}
Observable emits value whetenever it has new one.
could complete on throw error.

Subscribers: We define a function that is called with that value as an argument.

The process data function is likely to be triggers on another thread, so if we want to make UI updates we will have to remember to specify the thread just before the subscriber.We can use the **observeOn** opertator to switch all following operations and subscribers onto the thread specified.
We can define the results in Observable, the example showed previously is using the <Obervable<List<Entry>> getFeed(String url)
