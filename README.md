#NodeHtmlParser
A forgiving HTML parser written in JS for both the browser and NodeJS (yes, despite the name it works just fine in any modern browser). The parser can handle streams (chunked data) and supports custom handlers for writing custom DOMs/output.

##Running Tests

###Run tests under node:
node runtests.js

###Run tests in browser:
View runtests.html in any browser

##Usage In Node
``var htmlparser = require("node-htmlparser");
var rawHtml = "Xyz <script language= javascript>var foo = '<<bar>>';< /  script><!--<!-- Waah! -- -->";
var handler = new htmlparser.DefaultHandler(function (error) {
	if (error)
		[...do something for errors...]
	else
		[...parsing done, do something...]
});
var parser = new htmlparser.Parser(handler);
parser.ParseComplete(rawHtml);
sys.puts(sys.inspect(handler.dom, false, null));``

##Usage In Browser
``var handler = new Tautologistics.NodeHtmlParser.DefaultHandler(function (error) {
	if (error)
		[...do something for errors...]
	else
		[...parsing done, do something...]
});
var parser = new Tautologistics.NodeHtmlParser.Parser(handler);
parser.ParseComplete(document.body.innerHTML);
alert(JSON.stringify(handler.dom, null, 2));``

##Example output
``[ { raw: 'Xyz ', data: 'Xyz ', type: 'text' }
, { raw: 'script language= javascript'
  , data: 'script language= javascript'
  , type: 'script'
  , name: 'script'
  , attribs: { language: 'javascript' }
  , children: 
     [ { raw: 'var foo = \'<bar>\';<'
       , data: 'var foo = \'<bar>\';<'
       , type: 'text'
       }
     ]
  }
, { raw: '<!-- Waah! -- '
  , data: '<!-- Waah! -- '
  , type: 'comment'
  }
]``

##Streaming To Parser
		

##Handler Options
