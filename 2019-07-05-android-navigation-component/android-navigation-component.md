## Android JetPack: Navigation Component
Progression of architecture in Android, from having no guidance or indication from Google, using variations of the MVx patterns to the inclusion of JetPack since last year's Google IO.

Activities are an Android level component, like Content Providers, Broadcast Receivers, and Services, registered in AndroidManifest, UI facing elements created by Android system when system starts your app, starts an Activity, as an entry point.

> "Once we have gotten in to this entry-point to your UI, we really don't care how you organise the flow inside."
-- Dianne Hackborn, Android Framework team

Framework isn't opinionated, and does not care about the structure of your application.

Navigating around an application is a fundamental operation in Android, and forms the basis for the structure of your application.

In it's simplest form you would have an Android Activity, and would use an Intent to navigate from one to the other.

With Android 3.0 (Honeycomb) developers could break activities into subcomponents called Fragments in order to build richer, more interactive user interfaces.

This was often demonstrated with a master / detail interface, as a responsive layout for use with larger screens such as tablets, or large aspect phones.
 
Fragments would be added, or removed using fragment transactions, but would introduce a much more complex lifecycle behaviour than what we have been used to with Activities.

Furthermore, Fragment's complicate the back stack navigation, leading to edge cases where your stack is stale or invalid, and results in unexpected user behaviour on configuration change.

Since Fragment's are created by the framework, you don't have control over the initialisation, so setting properties might work at first, but will be null if the Fragment is recreated when the user returns to your application. 

Making communication between Fragment's or their host quite difficult, having to check for an interface implementation onAttach prior to the introduction of shared ViewModel's.

Sharing data between activities can be fairly difficult, as data needs to be Parcelable, and must hand over data from one to the other. Making it difficult to build larger scopes.

The only larger scope available to an activity is the application, which survives the entire duration of the user experience.

This is often also present when trying to build dependency graphs, where components such as repositories, databases, or network clients need to only be scoped to a flow of screens, and don't need to take up valuable memory space until the user is in your funnel.

Using an Activity as a larger scope with nested destination scopes, being able to share data across screens using ViewModel's or otherwise.

Fragments are an implementation of this destination concept, whilst mired with lifecycle issues, allowing the navigation component to handle the back stack makes this simple.

## Introducing the Navigation Component
A collection of libraries, a plugin, and tooling for unifying and simplifying Android Navigation.

Handles all the common facets of navigation patterns, including backstack, transactions, animations, deep links, and type safe arguments.

Works natively with Activity and Fragment, and with custom views should you wish to define your own destinations.

## Navigation Graph
Android Studio 3.3 introduces the new navigation editor, allowing you to utilise a graphical editor to build your application navigation graph.

Each screen is represented as a destination that shows how the navigation actions behave, and allow you to specify the arguments required for each screen which will allow to you pass type safe values.

You can also configure a deep link easily and simpliy.

## NavHostLayout
Simply a fragment widget that will act as a host for each of your fragment destinations, not compatible with Activity's. It makes sense to use Fragment's with the Navigation Library as you can easily navigate between screens and have the lifecycle, transactions, and configuration handled for you automatically.

## NavController
Each NavHostFragment has a controller that allows you to invoke navigation actions providing the necessary arguments and will perform the transactions as necessary.

## SafeArgs
When using the safeargs plugin in your project, you can add arguments to your destinations in your navigation graph to generate a type safe args class in Kotlin, that has default arguments and null safety to boot.

The navigation library also provides extensions for configuring BottomNavigationView simply and easily.

[Principles of Navigation]

[Migration to Navigation Component]