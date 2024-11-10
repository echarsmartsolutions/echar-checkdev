# Echar-Check
This hecktool will pool by IP or his Network name and returns the trip time in miliseconds as directly configured or by automated via <code>msg.payload</code> input command. It can be used as a triggered or timed configuration!
<dl class="message-properties">
        <dt>To a better result <span class="property-type">Best Practice</span></dt>
        <dd>Regarding network issues and traffic protections</dd>
        <dd style="color: darkred;">We will delay 100ms from each host to monitor</dd>
        <dd>this will help to keep in a safe way and not be kicked from the network trafic, caused of fully load the network bandwidth</dd>
        <dd>Ideal work scanning cyclically time window</dd><dd>consider to use <b><i>injection each 2seconds or more</i></b></dd>
        <dd>Ideal host quantities per cycle </dd><dd>keep <b><i>maximum 20 hosts</i></b></dd>
    </dl>
     <dt> <h3>Hash and Key </h3> <span class="property-type">Parameters</span></dt>
    <dd>If you have them, please fill-up the values on the right field.</dd>
    <dd>Key and Hash are needed to activate the communication process</dd>
    <dl class="message-properties">
        <dd>If you don't have it, please send a Telegram message to
        <b><code>@echarcheck2DerBot</code></b> with detail information:<br>
        <ul><li>Your information </li><li>UC20 / M3000 / M4000 Serial number.</li></ul>
        These informations are needed to we generate the proper Hash and Authorization Key!!</dd>
    </dl>
    <dt>Active your check node, online with Internet on port X1</dt>
    <dd>Set as triggered option, send a payload <pre>[{"host":"@echarcheck2DerBot","name":"Request"}]</pre>
        to the node, to complete the request, once you recieve the Telegram message in return, please fulfilled both values, with they inserted, you can activate the check node!!<br>
    if you have nany trouble, send email to <code>atendimento@echar.com.br</code></dd>
    <br>
    <p><b>The Pair Hash & Key will be the same to all used nodes</b></p>
    <ul>
        <li><b>Hash option</b><br>
            <p>Hash information to get from the supplier,
            this node will work only after properly set</p>
        </li>
        <li><b>Key option</b><br>
            <p>Unlock password to activate the node,
            this will allow the node to be activated</p>
        </li>
    </ul>   
    <h3>Output</h3>
    <dl class="message-properties">
        <dt>payload <span class="property-type">number</span></dt>
        <dd> the trip time in miliseconds, or boolean <i>false</i> if no response.</dd>
        <dt>topic <span class="property-type">string</span></dt>
        <dd> the target host or ip address.</dd>
        <dt>[monitor] <span class="property-type">object</span></dt>
        <dd> an object containing <code>host</code> and any other properties sent in the array object.<br>
            <b>Note</b>: This object is only appended when using triggered mode and an array for input payload. It is
            intended for advanced users and permits scenarios where you need additional properties to be tagged into your result for use downstream.</dd>
    </dl>
    <h3>Details</h3>
    <p>Returns <b>false</b> if no response received, or if the host is unresolveable.</p>
    <p>Default monitor is every 20 seconds but can be configured.</p>
    <h4>Protocol...</h4>
    <ul>
        <li><b>Automatic</b><br>
            <P>Will use any Protocol, IPv4 or IPv6, to reach host; based on your operating system network settings</P>
        </li>
        <li><b>IPv4</b><br>
            <P>Forces use of IPv4 to reach host. Will fail if no route availibe</P>
        </li>
        <li><b>IPv6</b><br>
            <P>Forces use of IPv6 to reach host. Will fail if no route availibe</P>
        </li>
    </ul>
    <h4>Mode...</h4>
    <ul>
        <li><b>Timed</b><br>
            <P>In Timed mode, the fields <code>Target</code> and <code>monitor (S)</code> must be populated.</P>
            <p>Target must be a CSV list of hosts / IPs e.g. <code>"192.168.0.1"</code> or <code>"192.168.0.1, www.google.com"</code></p>
            <p>monitor (S) is the number of seconds between monitors</p>
        </li>
        <li><b>Triggered</b><br>
            <p>In Triggered mode, you must connect an input wire and pass a <code>msg</code> in to trigger the monitor operation.</p>
            <p>If <code>Target</code> is populated, this will be used as the host/ip. The Target must be is a CSV list of
                hosts / IPs e.g. <code>"192.168.0.1"</code> or <code>"192.168.0.1, www.google.com"</code></p>
            <p>If Target is left empty, you can pass a CSV string or an array of hosts in <code>msg.payload</code>.
                <ul>
                    <li><b>string</b> - a CSV list of hosts / IPs e.g. <code>"192.168.0.1"</code> or <code>"192.168.0.1, www.google.com"</code> </li>
                    <li><b>array</b> - an array of hosts as strings or objects. <b>Note</b>: The object must contain at minimum <code>.host</code>.
                        Optionally, you can add a <code>timeout</code> property between 1000 & 30000 (default is 5000 / 5 seconds).
                        Additionally, you can add whatever other properties you wish to this object and when the monitor result is returned, it will
                        be passed to the next node in <code>msg.monitor</code> for use downstream</li>
                    <li>Example array payload input: <pre>[
    "192.168.0.99",
    {
        "host":"192.168.0.1",
        "name":"The router"
    },
    {
        "host":"myapiserver.com",
        "name":"external API",
        "timeout": 20000,
        "support":"support@myapiserver.com"
    }
]</pre>         </li>
                </ul>
            </p>
        </li>
    </ul>      
