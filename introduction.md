<h1 id="introduction">Introduction</h1>

<p>In this exercise, we'll set up our workstation and cloud environment so
that we're ready to build and run modern .NET applications.</p>
<p><strong>You should have the url and credentials for the Pivotal
Cloud Foundry (PCF) instance you will be using.</strong></p>

<p>Alternatively, you can sign up for a trial account of the hosted version
of PCF, called Pivotal Web Services (PWS):</p>

<ol>
<li>
<p>Go to <a href="http://run.pivotal.io" rel="noreferrer noopener">http://run.pivotal.io</a> and choose
&quot;sign up for free.&quot;</p>
</li>
<li>
<p>Fill out and submit the sign up form.</p>
</li>
<li>
<p>Go to the email account you provided and click on the verification email link.</p>
</li>
<li>
<p>Select &quot;claim free trial&quot; and provide your phone number.</p>
</li>
<li>
<p>Validate your account and create an organization.</p>
</li>
</ol>

<h1 id="install-cloud-foundry-cli">Install Cloud Foundry CLI</h1>
<p>You can interact with Cloud Foundry via a web GUI (Apps Manager), REST API, or
command line interface (CLI). To install the CLI follow the instructions at https://docs.pivotal.io/pivotalcf/cf-cli/install-go-cli.html.</p>

<p>Confirm that the CLI installed correctly by opening a command line terminal and
type: <code>cf -v</code></p>
</li>

<h1 id="install-net-core-and-visual-studio-code">Install .NET Core and Visual Studio Code</h1>
<p>.NET Core represents a modern way to build .NET apps, and here we make
sure we have everything needed to build ASP.NET Core apps.</p>
<ol>
<li>
<p>Visit <a href="https://www.microsoft.com/net/download" rel="noreferrer noopener">https://www.microsoft.com/net/download</a>
to download and install the latest version of the .NET Core SDK.</p>
</li>
<li>
<p>Confirm that it installed correctly by opening a command line and
type: <code>dotnet --version</code></p>
</li>
<li>
<p>Install <a href="https://code.visualstudio.com" rel="noreferrer noopener">Visual Studio Code</a> using
your favorite package manager.</p>
</li>
<li>
<p>Open Visual Studio Code and go to <strong>View → Extensions</strong></p>
</li>
<li>
<p>Search for <code>C#</code> and choose the top <code>C# for Visual Studio Code</code> option
and click <code>Install.</code> This gives you type-ahead support for C#.</p>
</li>
</ol>

<h1 id="create-an-aspnet-core-project">Create an ASP.NET Core project</h1>
<p>Visual Studio Code makes it easy to build new ASP.NET Core projects.
We'll create a sample project just to prove we can!</p>
<ol>
<li>
<p>Within Visual Studio Code, go to <strong>View → Integrated Terminal</strong>. The
Terminal gives you a shell interface without leaving Visual Studio Code.</p>
</li>
<li>
<p>Navigate to a location where you'll store your project files
(e.g. C:\BootcampLabs) and create a sub-directory called &quot;mvctest&quot; inside.</p>
</li>
<li>
<p>Navigate into the newly created &quot;mvctest&quot; directory and type in
<code>dotnet new mvc</code> to create a new ASP.NET Core MVC project.</p>
</li>
<li>
<p>In Visual Studio Code, click <strong>File → Open</strong> and navigate to the
directory containing the new ASP.NET Core project.</p>
</li>
<li>
<p>Observe the files that were automatically generated. Re-open the
Terminal window.</p>
</li>
<li>
<p>Start the project by typing <code>dotnet run</code> and visiting
<a href="http://localhost:5000" rel="noreferrer noopener">http://localhost:5000</a>. To stop the
application, enter <code>Ctrl+C</code>.</p>
</li>
</ol>

<h1 id="deploy-aspnet-core-application-to-cloud-foundry">Deploy ASP.NET Core application to Cloud Foundry</h1>
<p>Now let's deploy this app to Cloud Foundry!</p>
<ol>
<li>
<p>In Visual Studio Code, go to <strong>View → Extensions</strong>.</p>
</li>
<li>
<p>Search for &quot;Cloudfoundry&quot; and install
<code>Cloudfoundry Manifest YML support</code> extension. This gives type-ahead
support for Cloud Foundry manifest files.</p>
</li>
<li>
<p>In Visual Studio Code, create a new file called manifest.yml in the base
directory of your project (e.g. mvctest).</p>
</li>
<li>
<p>Open the <code>manifest.yml</code> file, and type in the following (notice the
typing assistance from the extension):</p>
 
```yaml
---
applications:
- name: core-cf-<enter your name>
  instances: 1
  memory: 256M
```
</li>
<li>
<p>In the Terminal, type in <code>cf login -a &lt;PCF API url&gt;</code> and provide
your credentials. Now you are connected to Pivotal Cloud Foundry.</p>
</li>
<li>
<p>Enter <code>cf push</code> into the Terminal, and watch your application get
bundled up and deployed to Cloud Foundry.</p>
</li>
<li>
<p>In Pivotal Cloud Foundry Apps Manager, see your app show up, and visit the app’s URL.</p>
</li>
</ol>

<h1 id="instantiate-spring-cloud-services-instances">Instantiate Spring Cloud Services instances</h1>

<p>Spring Cloud Services wrap up key Spring Cloud projects with managed capabilities.
Here we create a couple of these managed services.</p>
<ol>
<li>
<p>In Pivotal Cloud Foundry Apps Manager, select your &quot;space&quot; on the
left nav bar, and switch to the &quot;Services&quot; tab. Note that all of these
activities can also be done via the CF CLI.</p>
</li>
<li>
<p>Click &quot;Add Service.&quot;</p>
</li>
<li>
<p>Type &quot;Spring&quot; into the search box to narrow down the choices.</p>
</li>
<li>
<p>Select &quot;Service Registry&quot; and select the default plan.</p>
</li>
<li>
<p>Provide an instance name and do not choose to bind the service to
any existing applications. Select &quot;Create.&quot; This service will take a
couple of minutes to become available.</p>
</li>
<li>
<p>Repeat step 3 above and choose &quot;Config Server&quot; from the marketplace.</p>
</li>
<li>
<p>Choose the default plan, provide an instance name, and click
&quot;Create.&quot; Wait a couple minutes before expecting to see this service
fully operational.</p>
</li>
<li>
<p>Return to your default space in Apps Manager, click &quot;Services&quot;,
choose Service Registry, and click the &quot;manage&quot; link. This takes you to
the Eureka dashboard.</p>
</li>
<li>
<p>Return again to the default space, click &quot;Services&quot;, choose Config
Server, and click the &quot;manage&quot; link. Nothing here just yet!</p>
</li>
</ol>
