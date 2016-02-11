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
