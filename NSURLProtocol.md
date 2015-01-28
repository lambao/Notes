# Notes for using ios NSURLProtocol

1. If multiple nsurlprotocol is registered, the last one registered will be called first for canInitWithRequest method to check whether it can handle the request.

2. It is understandable that registered nsurlprotocol is consulted when loading a request. but what exactly is "loading a request". Actually, it means when create a new NSUrlConnection object instead of a new NSURLRequest boject. That is the reason why canonicalRequestForRequest can create a new request object without triggering the canInitWithRequest be called again.

3. NSURLProtocol.client represents the receiver who initialized the original request, and who expect to receive response data from NSURLProtocol instance if true was returned by the the instance. The receiver makes itself accessible through `NSURLProtocol.client` property with NSURLProtocolClient protocol.

4. When NSURLProtocol handles a request, it may need to create a new nsurlconnection instance to get server response, the new nsurlconnection instance will send out the new query to all registered NSUrlProtocol instance, and if the same NSUrlProtocol return true on its canInitWithRequest method, it will lead to an infinite loop. Usually this is handled by adding a particular flag in the request object by calling NSUrlProtocol's setProperty and propertyForKey method. So if the flag already exists, just skip it and let the NSURLConnection's default implementation to handle the request.

5. When a web request was sent from ios UIWebView, `NSUrlProtocol.canInitWithRequest` may be called multiple times for the same request. However, initWithRequest and startLoading should only be called once when the URL Loading system asks the selected NSUrlProtocol to process the request.

6. It is possible to chain multiple NSURLProtocol to handle the same request, the key is the lower level NSUrlProtocol's connection handler must call its `NSUrlProtocol.client` delegate method to pass the information to other NSUrlProtocol instances. For example, if one NSUrlProtocol instance does not know how to handle an authentication challenge, it should still return true to canAuthenticateAgainstProtectionSpace method, and then call `[[self client] URLProtocol:self didReceiveAuthenticationChallenge:challenge ];` method to let other NSUrlProtocol instance to handle it.

7. Be careful when deciding what scope to define properties or instance variables when implementing NSUrlProtocol, If the information is per request, then it should be defined as instance property or variable in NSUrlProtocol. However, there is no easy way to define per webview or per page variables as NSUrlProtocol alloc method is called from ios sytem, not the application code.

[Source](http://jonathanblog2000.blogspot.jp/2014/04/using-ios-nsurlprotocol.html)