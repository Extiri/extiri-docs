# Get snippet

```https://extiri.com/api/1/snippets/get/<snippet's id>```

Method: `GET`

This endpoint will return snippet with specified id.

## Parameters
- snippet's id (required) - id of snippet, for example: `C05D571B-E7F0-486D-98C9-7EF369F43CB7`

## Success response

- id - id of snippet.
- title - string containing title of snippet.
- desc - string containing description of snippet.
- code - string containing code of snippet.
- category - string containing one of predefined categories for snippet.
- language - string containing language key for language of code.
- creationDate - string containing ISO-8601 encoded date of snippet creation.
- isHidden - bool informing whether snippet should be shown.

## Example

Request:

```https://extiri.com/api/1/snippets/get/C05D571B-E7F0-486D-98C9-7EF369F43CB7```

Response:

```json
{
  "desc": "Loads website provided using URL. WebView loads a new website whenever URL is changed. Optional onLoadStart and onLoadFinish run when WebView starts loading website or finishes loading of website respectively. You can provide own WKWebView and then use it to control WebView (navigationDelegate will be replaced).",
  "code": "struct WebView: NSViewRepresentable {\n\t\/\/\/ URL of current page. If changed, WebView will change into new URL.\n\t@Binding var url: URL\n\t\n\tprivate var onLoadStart: (WKWebView) -> ()\n\tprivate var onLoadFinish: (WKWebView) -> ()\n\t\n\tprivate var wkWebView: WKWebView\n\t\n\tinit(url: Binding<URL>, wkWebView: WKWebView = WKWebView(), onLoadStart: ((WKWebView) -> ())? = nil, onLoadFinish: ((WKWebView) -> ())? = nil) {\n\t\tself.wkWebView = wkWebView\n\t\t\n\t\tself._url = url\n\t\t\n\t\tif let onLoadStart = onLoadStart {\n\t\t\tself.onLoadStart = onLoadStart\n\t\t} else {\n\t\t\tself.onLoadStart = { _ in }\n\t\t}\n\t\t\n\t\tif let onLoadFinish = onLoadFinish {\n\t\t\tself.onLoadFinish = onLoadFinish\n\t\t} else {\n\t\t\tself.onLoadFinish = { _ in }\n\t\t}\n\t}\n\t\n\tfunc makeNSView(context: Context) -> WKWebView {\n\t\twkWebView.navigationDelegate = context.coordinator\n\t\twkWebView.load(URLRequest(url: url))\n\t\t\n\t\treturn wkWebView\n\t}\n\t\n\tfunc updateNSView(_ nsView: WKWebView, context: Context) {\n\t\tnsView.load(URLRequest(url: url))\n\t}\n\t\n\tfunc makeCoordinator() -> Coordinator {\n\t\tCoordinator(onLoadStart: onLoadStart, onLoadFinish: onLoadFinish)\n\t}\n\t\n\tclass Coordinator: NSObject, WKNavigationDelegate {\n\t\tlet onLoadStart: (WKWebView) -> ()\n\t\tlet onLoadFinish: (WKWebView) -> ()\n\t\t\n\t\tinit(onLoadStart: @escaping (WKWebView) -> (), onLoadFinish: @escaping (WKWebView) -> ()) {\n\t\t\tself.onLoadStart = onLoadStart\n\t\t\tself.onLoadFinish = onLoadFinish\n\t\t}\n\t\t\n\t\tfunc webView(_ webView: WKWebView, didCommit navigation: WKNavigation!) {\n\t\t\tonLoadStart(webView)\n\t\t}\n\t\t\n\t\tfunc webView(_ webView: WKWebView, didFinish navigation: WKNavigation!) {\n\t\t\tonLoadFinish(webView)\n\t\t}\n\t}\n}\n",
  "id": "32F585DE-C9F1-4A51-83F4-E3EA38D8CA3B",
  "category": "None",
  "title": "WKWebView swiftUI wrapper",
  "language": "swift",
  "creationDate": "2022-06-19T17:17:50Z",
  "creator": "2AAA76CF-87D8-4446-83BF-C22B9AEF531F",
  "isHidden": false
}
```