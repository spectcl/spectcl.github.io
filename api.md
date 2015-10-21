---

---

## Members
<dl>
<dt><a href="#expect_out">expect_out</a></dt>
<dd><p>Output object accessible by the user.
buffer contains all data on the stream between the previous two matches.
This object is meant to emulate TCL Expect&#39;s expect_out behavior.
For more, see <a href="http://www.tcl.tk/man/expect5.31/expect.1.html">http://www.tcl.tk/man/expect5.31/expect.1.html</a></p>
</dd>
<dt><a href="#options">options</a></dt>
<dd><p>Options object.</p>
</dd>
<dt><a href="#emitter">emitter</a></dt>
<dd><p>Spectcl is an emitter.</p>
</dd>
<dt><a href="#cache">cache</a></dt>
<dd><p>String containing the data to match against thus far.
Subject to matchMax restrictions.
Once a match is found, the contents up to the match are flushed to
expect_out.buffer.</p>
</dd>
<dt><a href="#cacheStream">cacheStream</a></dt>
<dd><p>A buffering stream.  STDOUT/ERR is piped to this stream.
Starts out paused, and is resumed when we are expecting, and is
paused again when we match.  We also watch this stream for eof.</p>
</dd>
<dt><a href="#child">child</a></dt>
<dd><p>Child object.</p>
</dd>
<dt><a href="#expecting">expecting</a></dt>
<dd><p>True if this session is currently in an expect block.</p>
</dd>
<dt><a href="#fullBuffer">fullBuffer</a></dt>
<dd><p>Set when the cache string is longer than options.matchMax</p>
</dd>
<dt><a href="#EXP_CONTINUE">EXP_CONTINUE</a></dt>
<dd><p>Enum values for special handling</p>
</dd>
</dl>
## Functions
<dl>
<dt><a href="#spawn">spawn(command, [cmdParams], [cmdOptions], [spawnOptions])</a> ⇒ <code>undefined</code></dt>
<dd><p>Spawns the Expect session&#39;s child process</p>
</dd>
<dt><a href="#expect">expect(expArr, cb)</a> ⇒ <code>undefined</code></dt>
<dd><p>Wait until:</p>
<ol>
<li>One of the patterns matches the output of the spawned process</li>
<li>A specified time period has passed</li>
<li>End-of-file is seen
After one of the above conditions is met, the provided callback will be called.</li>
</ol>
</dd>
<dt><a href="#send">send(data)</a> ⇒ <code>undefined</code></dt>
<dd><p>Sends data to the spawned process</p>
</dd>
<dt><a href="#sendEof">sendEof()</a> ⇒ <code>undefined</code></dt>
<dd><p>Destroy the spawned process&#39; stdin stream.
Useful when working with apps that use inquirer.</p>
</dd>
<dt><a href="#on">on()</a> ⇒ <code>undefined</code></dt>
<dd><p>Spectcl is an emitter.</p>
</dd>
<dt><a href="#once">once()</a> ⇒ <code>undefined</code></dt>
<dd><p>Spectcl is an emitter.</p>
</dd>
<dt><a href="#emit">emit()</a> ⇒ <code>undefined</code></dt>
<dd><p>Spectcl is an emitter.</p>
</dd>
<dt><a href="#removeListener">removeListener()</a> ⇒ <code>undefined</code></dt>
<dd><p>Spectcl is an emitter.</p>
</dd>
</dl>
<a name="expect_out"></a>
## expect_out
Output object accessible by the user.
buffer contains all data on the stream between the previous two matches.
This object is meant to emulate TCL Expect's expect_out behavior.
For more, see http://www.tcl.tk/man/expect5.31/expect.1.html

**Kind**: global variable  
<a name="options"></a>
## options
Options object.

**Kind**: global variable  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| timeout | <code>number</code> | Max inactivity time, in ms. Defaults to 30s |
| matchMax | <code>number</code> | Max length of cache. Default to 2000 |

<a name="emitter"></a>
## emitter
Spectcl is an emitter.

**Kind**: global variable  
<a name="cache"></a>
## cache
String containing the data to match against thus far.
Subject to matchMax restrictions.
Once a match is found, the contents up to the match are flushed to
expect_out.buffer.

**Kind**: global variable  
<a name="cacheStream"></a>
## cacheStream
A buffering stream.  STDOUT/ERR is piped to this stream.
Starts out paused, and is resumed when we are expecting, and is
paused again when we match.  We also watch this stream for eof.

**Kind**: global variable  
<a name="child"></a>
## child
Child object.

**Kind**: global variable  
<a name="expecting"></a>
## expecting
True if this session is currently in an expect block.

**Kind**: global variable  
<a name="fullBuffer"></a>
## fullBuffer
Set when the cache string is longer than options.matchMax

**Kind**: global variable  
<a name="EXP_CONTINUE"></a>
## EXP_CONTINUE
Enum values for special handling

**Kind**: global variable  
<a name="spawn"></a>
## spawn(command, [cmdParams], [cmdOptions], [spawnOptions]) ⇒ <code>undefined</code>
Spawns the Expect session's child process

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| command | <code>string</code> &#124; <code>Array</code> | The command to spawn.  If string, will be split on ' ' if params not provided. |
| [cmdParams] | <code>Array</code> | Argv to pass to the child process. |
| [cmdOptions] | <code>Object</code> | Options used when spawning the child. |
| [spawnOptions] | <code>Object</code> | Options used when spawning the child. |
| spawnOptions.noPty | <code>boolean</code> | If true, spectcl will spawn the child directly, without obtaining a pty session. |

<a name="spawn..onData"></a>
### spawn~onData(data) ⇒ <code>undefined</code>
Preprocesses the `data` from `child`.
Evaluates the processed lines:
1. Stripping ANSI colors (if necessary)
2. Removing case sensitivity (if necessary)

**Kind**: inner method of <code>[spawn](#spawn)</code>  
**Emits**: <code>[data](#Spectcl+event_data)</code>  

| Param | Type | Description |
| --- | --- | --- |
| data | <code>String</code> &#124; <code>Object</code> | Data to process |

<a name="expect"></a>
## expect(expArr, cb) ⇒ <code>undefined</code>
Wait until:
1. One of the patterns matches the output of the spawned process
2. A specified time period has passed
3. End-of-file is seen
After one of the above conditions is met, the provided callback will be called.

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| expArr | <code>Array</code> | An array of even length, of the form: [{RegExp|String}, {Spectcl~handlerCallback}, {RegExp|String}, {Spectcl~handlerCallback}, ... ] |
| cb | <code>[expectFinalCallback](#Spectcl..expectFinalCallback)</code> | Callback to handle the response |

**Example**  
```js
// Watch for a '#' prompt
spectcl.expect([/#/, function(){ // called when we match on /#/ }])
```
<a name="send"></a>
## send(data) ⇒ <code>undefined</code>
Sends data to the spawned process

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| data | <code>string</code> | Data to send to the current spawned process. |

<a name="sendEof"></a>
## sendEof() ⇒ <code>undefined</code>
Destroy the spawned process' stdin stream.
Useful when working with apps that use inquirer.

**Kind**: global function  
<a name="on"></a>
## on() ⇒ <code>undefined</code>
Spectcl is an emitter.

**Kind**: global function  
<a name="once"></a>
## once() ⇒ <code>undefined</code>
Spectcl is an emitter.

**Kind**: global function  
<a name="emit"></a>
## emit() ⇒ <code>undefined</code>
Spectcl is an emitter.

**Kind**: global function  
<a name="removeListener"></a>
## removeListener() ⇒ <code>undefined</code>
Spectcl is an emitter.

**Kind**: global function  
