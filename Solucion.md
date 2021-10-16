# Deploying the system

In order to run the server we must do the following steps:

1.- Check whether we have installed Gradle and JDK in our computer.
To do it we can simply type 'gradle -v' and 'java -version' respectively.

2.- Once we have checked this, we can proceed to build and run the server
by executing the following commands:

```sh
./gradlew :server:build
./gradlew :server:bootRun
```

3.- At this point, server should be running and waiting for a client to connect,
so now we are able to build and run the client:

```sh
./gradlew :client:build
./gradlew :client:bootRun
```

# Finnishing server code

The sever code needed actions to be done after being requested to translate
some word. We could use an extern API to send the text to be translated, but
you need to pay to use most of them so we're going to add the translation directly:

```kt
@Endpoint
class TranslatorEndpoint {
    @PayloadRoot(namespace = TRANSLATOR_NAMESPACE_URI, localPart = "TranslationRequest")
    @ResponsePayload
    fun translation(@RequestPayload request: TranslationRequest): TranslationResponse = 
        TranslationResponse().apply{
            translation = "Tradúceme!"
        }
}
```