PHP HTTP Tools
=======================================

PHP HTTP Tool kit that brings common functionality in a standard way,
supporting PSR-7 and PSR-17.

Installation
---------------------------------------

Using composer.

```bash
composer install francerz/php-http-tools
```

Featured functionality
----------------------------------------

### HttpFactoryManager class

Preserve per instance, reference of PSR-17 Factories (psr/http-factory).
Uses set and get methods to manage existing factory instances.

#### Individual setter methods

- `setRequestFactory(RequestFactoryInterface $requestFactory)`
- `setResponseFactory(ResponseFactoryInterface $responseFactory)`
- `setServerRequestFactory(ServerRequestFactoryInterface $serverRequestFactory)`
- `setStreamFactory(StreamFactoryInterface $streamFactory)`
- `setUploadedFileFactory(UploadedFileFactoryInterface $uploadedFileFactory)`
- `setUriFactory(UriFactoryInterface $uriFactory)`

#### Getter methods

Getter Methods will throw a `LogicException` if not factory has been set
previously.
- `getRequestFactory() : RequestFactoryInterface`
- `getResponseFactory() : ResponseFactoryInterface`
- `getServerRequestFactory() : ServerRequestFactoryInterface`
- `getStreamFactory() : StreamFactoryInterface`
- `getUploadedFileFactory() : UploadedFileFactoryInterface`
- `getUriFactory() : UriFactoryInterface`

#### Automatic setter method

The method `setMatchingFactories($factoryObject)` receives an object and
checks implementation of each Factory Interface. All matching interfaces
will be set.

This method is included on the constructor to quick factory setting.

### UriHelper class

Provides methods for common manipulation to `UriInterface` objects.

#### Creating uri of current request

- `getCurrent(UriFactoryInterface $uriFactory) : UriInterface`

#### Path part manipulation

- `appendPath(UriInterface $uri, string $postpath) : UriInterface`
- `prependPath(UriInterface $uri, string $prepath) : UriInterface`

#### Query part manipulation

- `withQueryParams(UriInterface $uri, string $key, $value) : UriInterface`
- `withQueryParams(UriInterface $uri, array $params, $replace = true) : UriInterface`
- `withoutQueryParam(UriInterface $uri, string $key, &$value = null) : UriInterface`
- `getQueryParams(UriInterface $uri) : array`
- `getQueryParam(UriInterface $uri, string $key) : ?string`

#### Fragment part manipulation

- `withFragmentParam(UriInterface $uri, string $key, $value) : UriInterface`
- `withFragmentParams(UriInterface $uri, array $params, $replace = true) : UriInterface`
- `withoutFragmentParam(UriInterface $uri, string $key, &$value = null) : UriInterface`
- `getFragmentParams(UriInterface $uri) : array`
- `getFragmentParam(UriInterface $uri, string $key) : ?string`

### MessageHelper class

Provides methods for common manipulation to `MessageInterface` objects.

#### Helper setup

- `setHttpFactoryManager(HttpFactoryManager $factories)`
- `setAuthenticationSchemes(array $authenticationSchemeClasses)`

#### Creating a request object from server parameters

- `getCurrentRequest() : RequestInterface`

#### Handling message headers

- `getAuthorizationHeader(MessageInterface $message) : ?AbstractAuthorizationHeader`

#### Parsing body message content based on Content-Type header

- `getContent(MessageInterface $message)`
- `withContent(MessageInterface $message, string $mediaType, $content) : MessageInterface`