# TCP / IP Server Client Example Part 1
## Requires
- Visual Studio 2012
## License
- MS-LPL
## Technologies
- C#
- vb
- Win32
- Windows Forms
- WPF
- Microsoft Azure
- .NET Framework
- Visual Basic .NET
- VB.Net
- .NET Framework 4.0
- Windows General
- Windows Phone
- C# Language
- VB.NET Language Features
- WinForms
- Windows 8
- Visual Studio 2012
- Windows Phone 8
- Windows Store app
## Topics
- Interop
- Controls
- Animation
- Graphics
- C#
- Data Binding
- Asynchronous Programming
- Security
- GDI+
- Authentication
- ASP.NET
- File System
- Class Library
- User Interface
- Games
- Windows Forms
- Serialization
- Architecture and Design
- Multithreading
- Navigation
- Microsoft Azure
- Data Access
- threading
- Powershell
- Images
- customization
- Media
- custom controls
- Web Services
- Windows Form Controls
- 2d graphics
- Performance
- Search
- VB.Net
- Parallel Programming
- Image manipulation
- Code Sample
- Word
- Image Gallery
- Printing
- Image
- Console Window
- .NET 4
- Imaging
- Drawing
- How to
- UI Design
- Generic C# resuable code
- File Systems
- Networking
- Windows PowerShell
- Image Optimization
- general
- Windows 8
- Windows Forms Controls
- C# Language Features
- Language Samples
- Graphics Functions
- Audio and video
- Devices and sensors
- Windows web services
- User Experience
- BitmapImage
- Windows Store app
- Load Image
## Updated
- 12/17/2013
## Description

<p>&nbsp;</p>
<div style="border:none; border-bottom:solid #595959 1.0pt; padding:0cm 0cm 1.0pt 0cm">
<h1><span><span>1<span style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span><span>Introduction</span></h1>
</div>
<p class="MsoNormal"><span>In this series we are going to be looking at TCP IP, Client / Servers and what a massive world of opportunities this knowledge opens up to us, from Chat and Video Conferencing, to Invisible process communication, and even Service
 Management. But today let&rsquo;s get the framework done.</span></p>
<div style="border:none; border-bottom:solid #595959 1.0pt; padding:0cm 0cm 1.0pt 0cm">
<h1><span><span>2<span style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span><span>Building the Sample</span></h1>
</div>
<p class="MsoNormal"><span>The sample is built in Visual Studio 2012 Ultimate as an x86 targeted application using .Net Framework 4. We will be using NuGet packages, a number of 3rd party libraries. All of which will be fully explained to you ensuring that
 the final compilation of your App will be hassle free. Oh! And the sample code is verbosely commented so you should have no problem in working out what the code does.</span></p>
<div style="border:none; border-bottom:solid #595959 1.0pt; padding:0cm 0cm 1.0pt 0cm">
<h1><span><span>3<span style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span><span>Description</span></h1>
</div>
<p class="MsoNormal"><span>Communication is fundamental to us all. But it is also fundamental to many programs. When your application connects with a database it has to communicate, when your browser connects to a website, it communicates and the vast majority
 of the communication that occurs on the internet is does through TCP communication. In this first example we will write a client and an &ldquo;echo server&rdquo; which simply replies with the message you sent &ndash; pretty much like the ping command. It doesn&rsquo;t
 sound like much but it is the basis that we will start from.</span></p>
<p class="MsoNormal"><span><img id="103976" src="103976-clientserver.png" alt="" width="714" height="188"><br>
</span></p>
<div style="border:none; border-bottom:solid #595959 1.0pt; padding:0cm 0cm 1.0pt 0cm">
<h1><span><span>4<span style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span><span>Creating our Application</span></h1>
</div>
<p class="MsoNormal"><span>Open Visual Studio 2012 and Create a New Project. Call the Project ClientApp. Now Click on the ClientApp Project in Solution Explorer and Add a New Project Called ServerApp. This makes it nice a simple for us to separate the Client
 and Server logic and code.</span></p>
<p class="MsoListParagraphCxSpFirst" style="text-indent:-18.0pt"><span><span>1.<span style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span><span>Change the form Text to Server and Client accordingly.</span></p>
<p class="MsoListParagraphCxSpLast" style="text-indent:-18.0pt"><span><span>2.<span style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span><span>The Server is a little more complicated than the Client so we will design that first</span></p>
<h2><span><span>4.1<span style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp; </span>
</span></span><span>The Server</span></h2>
<p class="MsoListParagraphCxSpFirst" style="text-indent:-18.0pt"><span style="font-size:9.5pt; line-height:107%; font-family:Symbol; color:black"><span>&middot;<span style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span><span style="font-size:9.5pt; line-height:107%; font-family:Consolas; color:black">Add a StatusStrip to the Server Form</span></p>
<p class="MsoListParagraphCxSpMiddle" style="margin-left:72.0pt; text-indent:-18.0pt">
<span style="font-size:9.5pt; line-height:107%; font-family:&quot;Courier New&quot;; color:black"><span>o<span style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;
</span></span></span><span style="font-size:9.5pt; line-height:107%; font-family:Consolas; color:black">Add two Labels to the StatusStrip and Set their Text Properties to</span></p>
<p class="MsoListParagraphCxSpMiddle" style="margin-left:108.0pt; text-indent:-18.0pt">
<span style="font-size:9.5pt; line-height:107%; font-family:Wingdings; color:black"><span>&sect;<span style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;
</span></span></span><span style="font-size:9.5pt; line-height:107%; font-family:Consolas; color:black">Number of Connections</span></p>
<p class="MsoListParagraphCxSpMiddle" style="margin-left:108.0pt; text-indent:-18.0pt">
<span style="font-size:9.5pt; line-height:107%; font-family:Wingdings; color:black"><span>&sect;<span style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;
</span></span></span><span style="font-size:9.5pt; line-height:107%; font-family:Consolas; color:black">0</span></p>
<p class="MsoListParagraphCxSpMiddle" style="margin-left:72.0pt; text-indent:-18.0pt">
<span style="font-size:9.5pt; line-height:107%; font-family:&quot;Courier New&quot;; color:black"><span>o<span style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;
</span></span></span><span style="font-size:9.5pt; line-height:107%; font-family:Consolas; color:black">Change the Second Labels Name to lblNumberOfConnections</span></p>
<p class="MsoListParagraphCxSpMiddle" style="text-indent:-18.0pt"><span style="font-size:9.5pt; line-height:107%; font-family:Symbol; color:black"><span>&middot;<span style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span><span style="font-size:9.5pt; line-height:107%; font-family:Consolas; color:black">Add a RichTextBox to the Form and Set it&rsquo;s Docking property to Fill</span></p>
<p class="MsoListParagraphCxSpLast" style="text-indent:-18.0pt"><span style="font-size:9.5pt; line-height:107%; font-family:Symbol; color:black"><span>&middot;<span style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span><span style="font-size:9.5pt; line-height:107%; font-family:Consolas; color:black">Name The RichTextBox rtbServer</span></p>
<h2><span><span>4.2<span style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp; </span>
</span></span><span>The Client</span></h2>
<p class="MsoListParagraphCxSpFirst" style="text-indent:-18.0pt"><span style="font-size:9.5pt; line-height:107%; font-family:Symbol; color:black"><span>&middot;<span style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span><span style="font-size:9.5pt; line-height:107%; font-family:Consolas; color:black">Add a RichTextBox to the Form and Set it&rsquo;s Docking property to Fill</span></p>
<p class="MsoListParagraphCxSpLast" style="text-indent:-18.0pt"><span style="font-size:9.5pt; line-height:107%; font-family:Symbol; color:black"><span>&middot;<span style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span><span style="font-size:9.5pt; line-height:107%; font-family:Consolas; color:black">Name The RichTextBox rtbClient</span></p>
<h2><span><span>4.3<span style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp; </span>
</span></span><span>Now to the Code</span></h2>
<p class="MsoNormal"><span>Ok now we have created our front ends, you can format the RichTextBoxes any way you like. We need to start our coding. Again we will start with the Server.</span></p>
<h2><span><span>4.4<span style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp; </span>
</span></span><span>Server Code</span></h2>
<p class="MsoNormal"><span>Our server does three things</span></p>
<p class="MsoListParagraphCxSpFirst" style="text-indent:-18.0pt"><span style="font-family:Symbol"><span>&middot;<span style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span><span>It waits until a client connects</span></p>
<p class="MsoListParagraphCxSpMiddle" style="text-indent:-18.0pt"><span style="font-family:Symbol">&nbsp;</span></p>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>C#</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span></div>
<span class="hidden">csharp</span>

<div class="preview">
<pre class="csharp">&nbsp;<span class="cs__keyword">this</span>.tcpListener&nbsp;=&nbsp;<span class="cs__keyword">new</span>&nbsp;TcpListener(IPAddress.Loopback,&nbsp;<span class="cs__number">3000</span>);&nbsp;<span class="cs__com">//&nbsp;Change&nbsp;to&nbsp;IPAddress.Any&nbsp;for&nbsp;internet&nbsp;wide&nbsp;Communication</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">this</span>.listenThread&nbsp;=&nbsp;<span class="cs__keyword">new</span>&nbsp;Thread(<span class="cs__keyword">new</span>&nbsp;ThreadStart(ListenForClients));&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">this</span>.listenThread.Start();</pre>
</div>
</div>
</div>
<div class="endscriptcode">&nbsp;</div>
<p><span>&middot;<span style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span>It Handles the client&rsquo;s connection and communication</span></p>
<p>&nbsp;</p>
<p class="MsoListParagraphCxSpLast" style="text-indent:-18.0pt"><span style="font-family:Symbol">&nbsp;</span></p>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>C#</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span></div>
<span class="hidden">csharp</span>

<div class="preview">
<pre class="csharp">&nbsp;<span class="cs__keyword">private</span>&nbsp;<span class="cs__keyword">void</span>&nbsp;ListenForClients()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">this</span>.tcpListener.Start();&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">while</span>&nbsp;(<span class="cs__keyword">true</span>)&nbsp;<span class="cs__com">//&nbsp;Never&nbsp;ends&nbsp;until&nbsp;the&nbsp;Server&nbsp;is&nbsp;closed.</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//blocks&nbsp;until&nbsp;a&nbsp;client&nbsp;has&nbsp;connected&nbsp;to&nbsp;the&nbsp;server</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TcpClient&nbsp;client&nbsp;=&nbsp;<span class="cs__keyword">this</span>.tcpListener.AcceptTcpClient();&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//create&nbsp;a&nbsp;thread&nbsp;to&nbsp;handle&nbsp;communication&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//with&nbsp;connected&nbsp;client</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;connectedClients&#43;&#43;;&nbsp;<span class="cs__com">//&nbsp;Increment&nbsp;the&nbsp;number&nbsp;of&nbsp;clients&nbsp;that&nbsp;have&nbsp;communicated&nbsp;with&nbsp;us.</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;lblNumberOfConnections.Text&nbsp;=&nbsp;connectedClients.ToString();&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Thread&nbsp;clientThread&nbsp;=&nbsp;<span class="cs__keyword">new</span>&nbsp;Thread(<span class="cs__keyword">new</span>&nbsp;ParameterizedThreadStart(HandleClientComm));&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;clientThread.Start(client);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}</pre>
</div>
</div>
</div>
<div class="endscriptcode">&nbsp;</div>
<p><span>&middot;<span style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span>It replies with the same message that it received (Echoes)</span></p>
<p>&nbsp;</p>
<p class="MsoListParagraphCxSpLast" style="text-indent:-18.0pt"><span>&nbsp;</span></p>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>C#</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span></div>
<span class="hidden">csharp</span>

<div class="preview">
<pre class="csharp">&nbsp;<span class="cs__keyword">private</span>&nbsp;<span class="cs__keyword">void</span>&nbsp;HandleClientComm(<span class="cs__keyword">object</span>&nbsp;client)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;TcpClient&nbsp;tcpClient&nbsp;=&nbsp;(TcpClient)client;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;NetworkStream&nbsp;clientStream&nbsp;=&nbsp;tcpClient.GetStream();&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">byte</span>[]&nbsp;message&nbsp;=&nbsp;<span class="cs__keyword">new</span>&nbsp;<span class="cs__keyword">byte</span>[<span class="cs__number">4096</span>];&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">int</span>&nbsp;bytesRead;&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">while</span>&nbsp;(<span class="cs__keyword">true</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bytesRead&nbsp;=&nbsp;<span class="cs__number">0</span>;&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">try</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//blocks&nbsp;until&nbsp;a&nbsp;client&nbsp;sends&nbsp;a&nbsp;message</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bytesRead&nbsp;=&nbsp;clientStream.Read(message,&nbsp;<span class="cs__number">0</span>,&nbsp;<span class="cs__number">4096</span>);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">catch</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//a&nbsp;socket&nbsp;error&nbsp;has&nbsp;occured</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">break</span>;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">if</span>&nbsp;(bytesRead&nbsp;==&nbsp;<span class="cs__number">0</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//the&nbsp;client&nbsp;has&nbsp;disconnected&nbsp;from&nbsp;the&nbsp;server</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;connectedClients--;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;lblNumberOfConnections.Text&nbsp;=&nbsp;connectedClients.ToString();&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">break</span>;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//message&nbsp;has&nbsp;successfully&nbsp;been&nbsp;received</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ASCIIEncoding&nbsp;encoder&nbsp;=&nbsp;<span class="cs__keyword">new</span>&nbsp;ASCIIEncoding();&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;Convert&nbsp;the&nbsp;Bytes&nbsp;received&nbsp;to&nbsp;a&nbsp;string&nbsp;and&nbsp;display&nbsp;it&nbsp;on&nbsp;the&nbsp;Server&nbsp;Screen</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">string</span>&nbsp;msg&nbsp;=&nbsp;encoder.GetString(message,&nbsp;<span class="cs__number">0</span>,&nbsp;bytesRead);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;WriteMessage(msg);&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;Now&nbsp;Echo&nbsp;the&nbsp;message&nbsp;back</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Echo(msg,&nbsp;encoder,&nbsp;clientStream);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;tcpClient.Close();&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}</pre>
</div>
</div>
</div>
<div class="endscriptcode">&nbsp;</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h2><span><span>4.5<span style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp; </span>
</span></span><span>Client Code</span></h2>
<p class="MsoNormal"><span>Our Client does three things</span></p>
<p class="MsoListParagraphCxSpFirst" style="text-indent:-18.0pt"><span style="font-family:Symbol"><span>&middot;<span style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span><span>It connects to the Server</span></p>
<p class="MsoListParagraphCxSpMiddle" style="text-indent:-18.0pt"><span style="font-family:Symbol">&nbsp;</span></p>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>C#</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span></div>
<span class="hidden">csharp</span>

<div class="preview">
<pre class="csharp">&nbsp;client.Connect(serverEndPoint);</pre>
</div>
</div>
</div>
<div class="endscriptcode">&nbsp;</div>
<p><span>&middot;<span style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span>It sends a message</span></p>
<p>&nbsp;</p>
<p class="MsoListParagraphCxSpLast" style="text-indent:-18.0pt"><span style="font-family:Symbol">&nbsp;</span></p>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>C#</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span></div>
<span class="hidden">csharp</span>

<div class="preview">
<pre class="csharp">&nbsp;NetworkStream&nbsp;clientStream&nbsp;=&nbsp;client.GetStream();&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ASCIIEncoding&nbsp;encoder&nbsp;=&nbsp;<span class="cs__keyword">new</span>&nbsp;ASCIIEncoding();&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">byte</span>[]&nbsp;buffer&nbsp;=&nbsp;encoder.GetBytes(msg);&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;clientStream.Write(buffer,&nbsp;<span class="cs__number">0</span>,&nbsp;buffer.Length);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;clientStream.Flush();&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;Receive&nbsp;the&nbsp;TcpServer.response.</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;Buffer&nbsp;to&nbsp;store&nbsp;the&nbsp;response&nbsp;bytes.</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Byte[]&nbsp;&nbsp;data&nbsp;=&nbsp;<span class="cs__keyword">new</span>&nbsp;Byte[<span class="cs__number">256</span>];</pre>
</div>
</div>
</div>
<div class="endscriptcode">&nbsp;</div>
<p><span>&middot;<span style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span>It displays the response</span></p>
<p>&nbsp;</p>
<p class="MsoListParagraphCxSpLast" style="text-indent:-18.0pt"><span>&nbsp;</span></p>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>C#</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span></div>
<span class="hidden">csharp</span>

<div class="preview">
<pre class="csharp">&nbsp;<span class="cs__com">//&nbsp;String&nbsp;to&nbsp;store&nbsp;the&nbsp;response&nbsp;ASCII&nbsp;representation.</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;String&nbsp;responseData&nbsp;=&nbsp;String.Empty;&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;Read&nbsp;the&nbsp;first&nbsp;batch&nbsp;of&nbsp;the&nbsp;TcpServer&nbsp;response&nbsp;bytes.</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Int32&nbsp;bytes&nbsp;=&nbsp;clientStream.Read(data,&nbsp;<span class="cs__number">0</span>,&nbsp;data.Length);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;responseData&nbsp;=&nbsp;System.Text.Encoding.ASCII.GetString(data,&nbsp;<span class="cs__number">0</span>,&nbsp;bytes);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;rtbClient.AppendText(Environment.NewLine&nbsp;&#43;&nbsp;<span class="cs__string">&quot;From&nbsp;Server:&nbsp;&quot;</span>&nbsp;&#43;&nbsp;responseData);</pre>
</div>
</div>
</div>
<div class="endscriptcode">&nbsp;</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h3><span><span>4.5.1<span style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;
</span></span></span><span>Source Code Files</span></h3>
<p class="MsoListParagraphCxSpFirst" style="text-indent:-18.0pt"><span style="font-family:Symbol"><span>&middot;<span style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span><em><span>Source code ClientApp:Form1.cs &ndash; The main interface to our Client application</span></em><span>&nbsp;</span></p>
<p class="MsoListParagraphCxSpLast" style="text-indent:-18.0pt"><span style="font-family:Symbol"><span>&middot;<span style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span><em><span>Source code ServerApp:Form1.cs &ndash; The main interface to our Server application</span></em><span>&nbsp;</span></p>
<p class="MsoNormal"><span>&nbsp;</span></p>
<p class="MsoNormal"><span>In the next of this series we shall start making things interesting!</span></p>
<div style="border:none; border-bottom:solid #595959 1.0pt; padding:0cm 0cm 1.0pt 0cm">
<h1><span><span>5<span style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span><span>More Information</span></h1>
</div>
<p class="MsoNormal"><span>To convert the solution to a previous version of Visual Studio you can use this free application:
</span><a href="http://vsprojectconverter.codeplex.com/"><span style="font-size:12.0pt; line-height:107%; font-family:&quot;Times New Roman&quot;,&quot;serif&quot;">http://vsprojectconverter.codeplex.com/</span></a><span> or download and use Visual Studio 2013 Express which is
 freely available from Microsoft from here: </span><a href="http://www.visualstudio.com/downloads/download-visual-studio-vs"><span style="font-size:12.0pt; line-height:107%; font-family:&quot;Times New Roman&quot;,&quot;serif&quot;">http://www.visualstudio.com/downloads/download-visual-studio-vs</span></a><span>.</span></p>
