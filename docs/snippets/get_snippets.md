# Get snippets

```https://extiri.com/api/1/snippets/?page=<page>&query=<search text>&language=<language>&creator=<creator's id>```

Method: `GET`

This endpoint will return snippets filtered with specified options.

## Parameters
- page (optional, default: 1) - integer from 1 to unspecified number; you can get number of all pages by dividing total number of snippets by 20 (number of snippets on one page).
- query (optional, default: none) - server will return snippets which codes, titles or descriptions contain specified query. If absent, returns all snippets.
- language (optional, default: none) - server will return snippets with specified language key. If absent, returns all snippets.
- creator (optional, default: none) - server will return snippets created by specified creator. It is a identifier of creators account. If absent, returns all snippets.

## Success response

- totalNumberOfResults - integer containing number of all snippets in database.
- page
    - metadata
        - page - number of current page.
        - total - total number of results on current page.
        - per - number of snippets per page.
    - items - array of snippets.
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

```https://extiri.com/api/1/snippets?language=swift&page=1```

Response:

```json
{
  "totalNumberOfResults": 4,
  "page": {
    "items": [
      {
        "category": "None",
        "desc": "Loads website provided using URL. WebView loads a new website whenever URL is changed. Optional onLoadStart and onLoadFinish run when WebView starts loading website or finishes loading of website respectively. You can provide own WKWebView and then use it to control WebView (navigationDelegate will be replaced).",
        "language": "swift",
        "creator": "2AAA76CF-87D8-4446-83BF-C22B9AEF531F",
        "code": "struct WebView: NSViewRepresentable {\n\t\/\/\/ URL of current page. If changed, WebView will change into new URL.\n\t@Binding var url: URL\n\t\n\tprivate var onLoadStart: (WKWebView) -> ()\n\tprivate var onLoadFinish: (WKWebView) -> ()\n\t\n\tprivate var wkWebView: WKWebView\n\t\n\tinit(url: Binding<URL>, wkWebView: WKWebView = WKWebView(), onLoadStart: ((WKWebView) -> ())? = nil, onLoadFinish: ((WKWebView) -> ())? = nil) {\n\t\tself.wkWebView = wkWebView\n\t\t\n\t\tself._url = url\n\t\t\n\t\tif let onLoadStart = onLoadStart {\n\t\t\tself.onLoadStart = onLoadStart\n\t\t} else {\n\t\t\tself.onLoadStart = { _ in }\n\t\t}\n\t\t\n\t\tif let onLoadFinish = onLoadFinish {\n\t\t\tself.onLoadFinish = onLoadFinish\n\t\t} else {\n\t\t\tself.onLoadFinish = { _ in }\n\t\t}\n\t}\n\t\n\tfunc makeNSView(context: Context) -> WKWebView {\n\t\twkWebView.navigationDelegate = context.coordinator\n\t\twkWebView.load(URLRequest(url: url))\n\t\t\n\t\treturn wkWebView\n\t}\n\t\n\tfunc updateNSView(_ nsView: WKWebView, context: Context) {\n\t\tnsView.load(URLRequest(url: url))\n\t}\n\t\n\tfunc makeCoordinator() -> Coordinator {\n\t\tCoordinator(onLoadStart: onLoadStart, onLoadFinish: onLoadFinish)\n\t}\n\t\n\tclass Coordinator: NSObject, WKNavigationDelegate {\n\t\tlet onLoadStart: (WKWebView) -> ()\n\t\tlet onLoadFinish: (WKWebView) -> ()\n\t\t\n\t\tinit(onLoadStart: @escaping (WKWebView) -> (), onLoadFinish: @escaping (WKWebView) -> ()) {\n\t\t\tself.onLoadStart = onLoadStart\n\t\t\tself.onLoadFinish = onLoadFinish\n\t\t}\n\t\t\n\t\tfunc webView(_ webView: WKWebView, didCommit navigation: WKNavigation!) {\n\t\t\tonLoadStart(webView)\n\t\t}\n\t\t\n\t\tfunc webView(_ webView: WKWebView, didFinish navigation: WKNavigation!) {\n\t\t\tonLoadFinish(webView)\n\t\t}\n\t}\n}\n",
        "isHidden": false,
        "creationDate": "2022-06-19T17:17:50Z",
        "id": "32F585DE-C9F1-4A51-83F4-E3EA38D8CA3B",
        "title": "WKWebView swiftUI wrapper"
      },
      {
        "category": "None",
        "desc": "URLSession wrapper for JavaScriptCore. Apply using jsContext.setObject(JSHTTPRequest.self, forKeyedSubscript: \"HTTPRequest\" as NSString).",
        "language": "swift",
        "creator": "2AAA76CF-87D8-4446-83BF-C22B9AEF531F",
        "code": "import Foundation\nimport JavaScriptCore\n\n@objc protocol JSHTTPRequestProtocol: JSExport {\n\tvar url: String { get set }\n\tvar method: String { get set }\n\tvar requestHeaders: [String: String] { get set }\n\t\n\tfunc setRequestHeader(_ key: String, _ value: String)\n\tfunc send(_ completionHandler: JSValue)\n\tstatic func `open`(_ url: String, _ method: String) -> JSHTTPRequest\n}\n\n@objc class JSHTTPRequest: NSObject, JSHTTPRequestProtocol {\n\tvar url: String\n\tvar method: String\n\tvar requestHeaders: [String : String] = [:]\n\t\n\tfunc setRequestHeader(_ key: String, _ value: String) {\n\t\trequestHeaders[key] = value\n\t}\n\t\n\tfunc send(_ completionHandler: JSValue) {\n\t\tif let url = URL(string: url) {\n\t\t\tvar request = URLRequest(url: url)\n\t\t\t\n\t\t\trequest.httpMethod = method\n\t\t\t\n\t\t\tfor (key, value) in requestHeaders {\n\t\t\t\trequest.setValue(value, forHTTPHeaderField: key)\n\t\t\t}\n\t\t\t\n\t\t\tlet task = URLSession.shared.dataTask(with: request) { data, response, error in\n\t\t\t\tif let error = error {\n\t\t\t\t\tAsyncMain {\n\t\t\t\t\t\tcompletionHandler.call(withArguments: [[\"statusCode\": 1, \"error\": error.localizedDescription]])\n\t\t\t\t\t}\n\t\t\t\t} else {\n\t\t\t\t\tif let data = String(data: data!, encoding: .utf8) {\n\t\t\t\t\t\tAsyncMain {\n\t\t\t\t\t\t\tcompletionHandler.call(withArguments: [[\"statusCode\": 0, \"data\": data]])\n\t\t\t\t\t\t}\n\t\t\t\t\t} else {\n\t\t\t\t\t\tAsyncMain {\n\t\t\t\t\t\t\tcompletionHandler.call(withArguments: [[\"statusCode\": 1, \"error\": \"Can't generate string, because encoding is probably different than UTF-8.\"]])\n\t\t\t\t\t\t}\n\t\t\t\t\t}\n\t\t\t\t}\n\t\t\t}\n\t\t\t\n\t\t\ttask.resume()\n\t\t} else {\n\t\t\tcompletionHandler.call(withArguments: [[\"statusCode\": 1,\"error\": \"Provided URL is not valid.\"]])\n\t\t}\n\t}\n\t\n\tclass func `open`(_ url: String, _ method: String) -> JSHTTPRequest {\n\t\treturn .init(url: url, method: method)\n\t}\n\t\n\trequired init(url: String, method: String) {\n\t\tself.url = url\n\t\tself.method = method\n\t}\n}\n",
        "isHidden": false,
        "creationDate": "2022-06-19T15:20:00Z",
        "id": "8FEAE0E7-46AA-4785-9C4C-9889F1D64150",
        "title": "HTTP request"
      },
      {
        "category": "None",
        "desc": "A class for converting numbers between hexadecimal, decimal and binary.",
        "language": "swift",
        "creator": "2AAA76CF-87D8-4446-83BF-C22B9AEF531F",
        "code": "class ConvertersManager {\n\tenum NumberType: String, CaseIterable {\n\t\tcase hexadecimal\n\t\tcase binary\n\t\tcase decimal\n\t}\n\t\n\tenum ConvertingError: Error {\n\t\tcase numberIsNotOfSpecifiedType\n\t\t\n\t\tvar localizedDescription: String {\n\t\t\tswitch self {\n\t\t\t\tcase .numberIsNotOfSpecifiedType:\n\t\t\t\t\treturn \"Provided number is not a number of specified type.\"\n\t\t\t\t}\n\t\t}\n\t}\n\t\n\tprivate func isNumber(_ number: String, type: NumberType) -> Bool {\n\t\tvar digits = \"\"\n\t\t\n\t\tswitch type {\n\t\t\tcase .hexadecimal:\n\t\t\t\tdigits = \"0123456789ABCDEF\"\n\t\t\tcase .binary:\n\t\t\t\tdigits = \"01\"\n\t\t\tcase .decimal:\n\t\t\t\tdigits = \"0123456789\"\n\t\t}\n\t\t\n\t\tfor digit in number {\n\t\t\tif !digits.contains(digit) {\n\t\t\t\treturn false\n\t\t\t}\n\t\t}\n\t\t\n\t\treturn true\n\t}\n\t\n\tprivate func toBinary(number: String, ofType type: NumberType) -> String {\n\t\tswitch type {\n\t\t\tcase .hexadecimal:\n\t\t\t\tvar result = \"\"\n\t\t\t\t\n\t\t\t\tfor digit in number {\n\t\t\t\t\tresult.append(hexadecimalDigitToBinaryNumber(digit: String(digit)))\n\t\t\t\t}\n\t\t\t\t\n\t\t\t\treturn result\n\t\t\tcase .binary:\n\t\t\t\treturn number\n\t\t\tcase .decimal:\n\t\t\t\treturn String(Int(number)!, radix: 2)\n\t\t}\n\t}\n\t\n\tprivate func toDecimal(number: String, ofType type: NumberType) -> String {\n\t\tswitch type {\n\t\t\tcase .hexadecimal:\n\t\t\t\treturn String(Int(toBinary(number: number, ofType: type), radix: 2)!)\n\t\t\tcase .binary:\n\t\t\t\treturn String(Int(number, radix: 2)!)\n\t\t\tcase .decimal:\n\t\t\t\treturn number\n\t\t}\n\t}\n\t\n\tprivate func toHexadecimal(number: String, ofType type: NumberType) -> String {\n\t\tswitch type {\n\t\t\tcase .hexadecimal:\n\t\t\t\treturn number\n\t\t\tcase .binary:\n\t\t\t\treturn String(fillMissingZerosForHexadecimalInBinary(string: number)).split(by: 4).map {\n\t\t\t\t\tbinaryNumberToHexadecimalDigit(digit: $0)\n\t\t\t\t}.joined()\n\t\t\tcase .decimal:\n\t\t\t\treturn String(fillMissingZerosForHexadecimalInBinary(string: String(Int(number)!, radix: 2))).split(by: 4).map {\n\t\t\t\t\tbinaryNumberToHexadecimalDigit(digit: $0)\n\t\t\t\t}.joined()\n\t\t}\n\t}\n\t\n\t\/**\n\t Converts provided number to number of other type.\n\t \n\t - Parameter number: The number that will be converted.\n\t - Parameter ofType: The type of the number, which is going to be converted.\n\t - Parameter toType: The type to which number will be converted.\n\t \n\t - Returns: A hexadecimal number.\n\t *\/\n\tfunc convert(number: String, ofType typeOfNumber: NumberType, toType resultType: NumberType) throws -> String {\n\t\tif !isNumber(number, type: typeOfNumber) {\n\t\t\tthrow ConvertingError.numberIsNotOfSpecifiedType\t\t}\n\t\t\n\t\tswitch resultType {\n\t\t\tcase .hexadecimal:\n\t\t\t\treturn toHexadecimal(number: number, ofType: typeOfNumber)\n\t\t\tcase .binary:\n\t\t\t\treturn toBinary(number: number, ofType: typeOfNumber)\n\t\t\tcase .decimal:\n\t\t\t\treturn toDecimal(number: number, ofType: typeOfNumber)\n\t\t}\n\t}\n\n\tprivate func fillMissingZerosForHexadecimalInBinary(string: String) -> String {\n\t\tif string.count % 4 == 0 {\n\t\t\treturn string\n\t\t} else {\n\t\t\tvar result = string\n\t\t\tvar count = string.count\n\t\t\t\n\t\t\twhile count % 4 != 0 {\n\t\t\t\tresult = \"0\" + result\n\t\t\t\tcount += 1\n\t\t\t}\n\t\t\t\n\t\t\treturn result\n\t\t}\n\t}\n\t\n\tprivate func hexadecimalDigitToBinaryNumber(digit: String) -> String {\n\t\tswitch digit {\n\t\t\tcase \"0\":\n\t\t\t\treturn \"0000\"\n\t\t\tcase \"1\":\n\t\t\t\treturn \"0001\"\n\t\t\tcase \"2\":\n\t\t\t\treturn \"0010\"\n\t\t\tcase \"3\":\n\t\t\t\treturn \"0011\"\n\t\t\tcase \"4\":\n\t\t\t\treturn \"0100\"\n\t\t\tcase \"5\":\n\t\t\t\treturn \"0101\"\n\t\t\tcase \"6\":\n\t\t\t\treturn \"0110\"\n\t\t\tcase \"7\":\n\t\t\t\treturn \"0111\"\n\t\t\tcase \"8\":\n\t\t\t\treturn \"1000\"\n\t\t\tcase \"9\":\n\t\t\t\treturn \"1001\"\n\t\t\tcase \"A\":\n\t\t\t\treturn \"1010\"\n\t\t\tcase \"B\":\n\t\t\t\treturn \"1011\"\n\t\t\tcase \"C\":\n\t\t\t\treturn \"1100\"\n\t\t\tcase \"D\":\n\t\t\t\treturn \"1101\"\n\t\t\tcase \"E\":\n\t\t\t\treturn \"1110\"\n\t\t\tcase \"F\":\n\t\t\t\treturn \"1111\"\n\t\t\tdefault:\n\t\t\t\t\/\/ Impossible to reach.\n\t\t\t\treturn \"Error: Invalid digit.\"\n\t\t}\n\t}\n\t\n\tprivate func binaryNumberToHexadecimalDigit(digit: String) -> String {\n\t\tswitch digit {\n\t\t\tcase \"0000\":\n\t\t\t\treturn \"0\"\n\t\t\tcase \"0001\":\n\t\t\t\treturn \"1\"\n\t\t\tcase \"0010\":\n\t\t\t\treturn \"2\"\n\t\t\tcase \"0011\":\n\t\t\t\treturn \"3\"\n\t\t\tcase \"0100\":\n\t\t\t\treturn \"4\"\n\t\t\tcase \"0101\":\n\t\t\t\treturn \"5\"\n\t\t\tcase \"0110\":\n\t\t\t\treturn \"6\"\n\t\t\tcase \"0111\":\n\t\t\t\treturn \"7\"\n\t\t\tcase \"1000\":\n\t\t\t\treturn \"8\"\n\t\t\tcase \"1001\":\n\t\t\t\treturn \"9\"\n\t\t\tcase \"1010\":\n\t\t\t\treturn \"A\"\n\t\t\tcase \"1011\":\n\t\t\t\treturn \"B\"\n\t\t\tcase \"1100\":\n\t\t\t\treturn \"C\"\n\t\t\tcase \"1101\":\n\t\t\t\treturn \"D\"\n\t\t\tcase \"1110\":\n\t\t\t\treturn \"E\"\n\t\t\tcase \"1111\":\n\t\t\t\treturn \"F\"\n\t\t\tdefault:\n\t\t\t\t\/\/ Impossible to reach.\n\t\t\t\treturn \"Error: Invalid digit.\"\n\t\t}\n\t}\n}",
        "isHidden": false,
        "creationDate": "2022-06-19T15:11:21Z",
        "id": "7AE81089-EF1C-465F-9C39-25115DCED320",
        "title": "Number converter"
      }
    ],
    "metadata": {
      "page": 1,
      "total": 3,
      "per": 20
    }
  }
}
```

