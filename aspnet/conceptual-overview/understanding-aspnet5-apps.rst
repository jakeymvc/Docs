ASP.NET 5 웹 앱 이해하기
======================

By `Steve Smith`_

ASP.NET 5 introduces several new fundamental concepts of web programming that are important to understand in order to productively create web apps. These concepts are not necessarily new to web programming in general, but are new to ASP.NET and thus are likely new to many developers whose experience with web programming has mainly been using ASP.NET and Visual Studio.

ASP.NET 5는 새롭게 몇 가지 근본적인 개념을 도입했는데 웹 앱을 생산적으로 작성하는데 이 개념들을 이해하는 것이 아주 중요하다. 이 개념들은 일반적으로 웹 프로그래밍에 있어 꼭 새롭다고 할 수는 없지만 ASP.NET 차원에서는 새롭다고 할 수 있다. 따라서, ASP.NET 과 비주얼스튜디오를 사용해서 웹 프로그래밍을 해왔던 개발자들에게는 새로운 개념일 가능성이 농후하다.

In this article:
	- `ASP.NET Project Structure`_
	- `Framework Target`_
	- `The project.json File`_
	- `The global.json File`_
	- `The wwwroot folder`_
	- `Client Side Dependency Management`_
	- `Server Side Dependency Management`_
	- `Configuring the Application`_
	- `Application Startup`_


.. `View or download <https://github.com/aspnet/docs/tree/master/docs/conceptual-overview/understanding-aspnet5-apps/sample>`_ the finished source from the project created in this article.

.. 이 글에서 작성한 완성된 코드는 `이 곳  <https://github.com/aspnet/docs/tree/master/docs/conceptual-overview/understanding-aspnet5-apps/sample>`_ 에서 확인할 수 있다.

ASP.NET Project Structure
-------------------------

ASP.NET 5's project structure adds new concepts and replaces some legacy elements found in previous versions of ASP.NET projects. The new default web project template creates a solution and project structure like the one shown here: 

ASP.NET 5 프로젝트는 프로젝트 구성에 있어 새로운 개념을 추가했을뿐 아니라 이전 버전의 레거시 요소도 바꿨다. 새로운 웹 프로젝트 템플릿은 아래 그림과 같이 솔루션과 프로젝트 구조를 잡는다.

.. image:: understanding-aspnet5-apps/_static/solution-explorer.png

The first thing you may notice about this new structure is that it includes a Solution Items folder with a *global.json* file, and the web 
project itself is located within a *src* folder within the solution. The new structure also includes a special *wwwroot* folder and a 
Dependencies section in addition to the References section that was present in past versions of ASP.NET (but which has been updated in this 
version). In the root the project there are also several new files such as *bower.json, config.json, gulpfile.js, package.json, project.json*, 
and *Startup.cs*. You may notice that the files *global.asax, packages.config*, and *web.config* are gone. In previous versions of 
ASP.NET, a great deal of application configuration was stored in these files and in the project file. In ASP.NET 5, this information and logic 
has been refactored into files that are generally smaller and more focused.

새로운 구조에서 처음으로 눈에 띄는 것은 *global.json* 파일을 포함하는 Solution Items 폴더와 웹 프로젝트를 품고 있는  *src* 폴더의 존재이다. 새로운 구조는 또한 *wwwroot* 라는 특별한 폴더와 Dependency 라는 섹션을 갖고 있다. Reference 섹션은 이전 버전에서 있던 개념이지만 새 버전에서 업데이트되었다. 프로젝트의 루트에는  *bower.json, config.json, gulpfile.js, package.json, project.json*, *Startup.cs* 파일들이 있다. 반면에 *global.asax, packages.config*, *web.config* 들은 사라졌다. 이전 버전의 ASP.NET 에서는 상당수의 설정이 이들 파일과 프로젝트 파일에 보관되어 있었다. ASP.NET 5에서는 이들 정보와 로직이 좀더 작고 용도가 뚜렷한 파일들로 재구성되었다.

Framework Target
----------------

ASP.NET 5 can target multiple frameworks, allowing the application to be deployed into different hosting environments. By default applications will target the full version of .NET, but they can also target the .NET Core. Most legacy apps will target the full ASP.NET 5, at least initially, since they're likely to have dependencies that include framework base class libraries that are not available in .NET Core today. .NET Core is a small version of the .NET framework that is optimized for web apps and supports Linux and Mac environments. It can be deployed with an application, allowing multiple apps on the same server to target different versions of .NET Core. It is also modular, allowing additional functionality to be added only when it is required, as separate NuGet packages (:doc:`learn more about .NET Core <dotnetcore>`).

ASP.NET 5는 여러 프레임워크를 대상으로 개발이 가능하기 때문에 애플리케이션을 다른 종류의 호스팅 환경에 배포할 수 있다. 기본적으로 애플리케이션은 .NET 풀 버전을 대상으로 하지만 닷넷 코어로 대상을 변경할 수 있다. 대부분의 레거시 앱들은 닷넷 코어에서 지원하지 않는 BCL에 의존하고 있을 가능성이 크기 때문에 적어도 초기에는 풀 버전 ASP.NET 5를 대상으로 할 것이다.  닷넷 코어는 웹 앱에 최적화된 경량 버전의 프레임워크이고 리눅스와 맥 환경을 지원한다. 닷넷 코어는 애플리케이션과 함께 배포될 수 있어 다른 버전의 닷넷 코어를 대상으로 하는 앱들이 동일 서버에서 동작할 수 있다. 이 것은 또한 별도 NuGet 패키지인 모듈로써 필요에 의해 기능을 추가할 수 있다 (:doc:`learn more about .NET Core <dotnetcore>`). 

You can see which framework is currently being targeted in the web application project's properties, by right-clicking on the web project in Solution Explorer and selecting Properties:

아래 그림과 같이 웹 애플리케이션의 속성에서 현재 설정하고 있는 대상 프레임워크를 확인할 수 있다. 솔루션 탐색기의 웹 프로젝트에서 오른쪽 마우스 버튼을 클릭하여 속성을 선택한다.
 
.. image:: understanding-aspnet5-apps/_static/project-properties.png

By default, the checkbox for *Use specific DNX version* is unchecked. To target a specific version, check the box and choose the appropriate *Version*, *Platform*, and *Architecture*.

기본적으로 *Use specific DNX version* 체크박스가 선택되어 있지 않다. 특정 버전을 대상으로 하려면 체크박스를 체크하고 원하는 *Version*, *Platform*, *Architecture* 를 선택한다.


The project.json File
---------------------

The project.json file is new to ASP.NET 5. It is used to define the project's `server side dependencies`_ (discussed below), as well as other project-specific information. The sections included in *project.json* by default with the default web project template are shown below.

project.json 파일은 ASP.NET 5에 새롭게 등장했다. 이 파일은 아래에서 논의하고 있는 `server side dependencies`_ 를 정의하는데 사용될 뿐만 아니라 프로젝트에 특화된 다른 정보도 정의한다. 웹 프로젝트 템플릿에 의해 기본적으로 작성된 *project.json* 파일의 섹션은 아래와 같다.

.. image:: understanding-aspnet5-apps/_static/project-json.png

The **webroot** section specifies the folder that should act as the root of the web site, which by convention defaults to `the wwwroot folder`_. The version property specifies the current version of the project. You can also specify other metadata about the project such as **authors** and **description**.

**webroot** 섹션은 웹 사이트의 루트로써 동작하는 폴더를 지정한다. 네이밍에 의한 기본 값은 `wwwroot`_ 폴더이다. version 속성은 프로젝트의 현재 버전을 정의한다. 또한, **authors** 와 **description** 같은 프로젝트의 메타데이터도 정의할 수 있다.

ASP.NET 5 has a great deal of support for command line tooling, and the **commands** section allows you to configure what certain command line commands should do (for instance, launch a web site or run tests).

ASP.NET 5는 커맨드 명령 도구를 상당히 잘 지원한다. **commands** 섹션은 개발자로 하여금 어떤 명령어를 통해 웹 사이트를 구동해야 할지, 테스트를 실행해야 할지 구성할 수 있게 해준다.

.. code-block:: javascript

    "commands": {
        "web": "Microsoft.AspNet.Hosting --server Microsoft.AspNet.Server.WebListener --server.urls http://localhost:5000",
        "gen": "Microsoft.Framework.CodeGeneration",
        "ef": "EntityFramework.Commands"
    },


The **frameworks** section designates which targeted frameworks will be built, and what dependencies need to be included. For instance, if you were using LINQ and collections, you could ensure these were included with your .NET Core build by adding them to the ``dnxcore50`` list of dependencies as shown.

**See Also:** `Diagnosing dependency issues with ASP.NET 5 <http://davidfowl.com/diagnosing-dependency-issues-with-asp-net-5/>`_

**frameworks** 섹션은 어떤 프레임워크를 대상으로 앱을 빌드할지, 어떤 종속성이 추가되어야 하는지 지정하도록 고정된 섹션이다. 예를 들어, LINQ와 컬렉션들을 사용하고 있다면 여러분의 앱에 닷넷 코어와 함께 ``dnxcore50`` 리스트에 해당 내용이 추가되어야 한다.

**참고:** `Diagnosing dependency issues with ASP.NET 5 <http://davidfowl.com/diagnosing-dependency-issues-with-asp-net-5/>`_


.. TODO Update this section

The **exclude** section is used to identify files and folders that should be excluded from builds. Likewise, **bundleExclude** is used to identify content portions of the project that should be excluded when bundling the site (for example, in production).

**exclude** 섹션은 빌드에서 제외하고자 하는 파일과 폴더를 식별하는데 쓰인다. 마찬가지로,  **bundleExclude** 섹션은 사이트(예를 들면, 운영 시스템)를 빌드할 때, 어떤 컨텐츠를 제외할지 식별하는데 쓰인다. 

.. image:: understanding-aspnet5-apps/_static/excludes.png

The **scripts** section is used to specify when certain build automation scripts should run. Visual Studio now has built-in support for running such scripts before and after certain events. The default ASP.NET project template has scripts in place to run during *postrestore* and *prepare* that install `client side dependencies`_ using npm and bower.

**scripts** 섹션은 특정 빌드 자동화 스크립트들이 실행되도록 지정한다. 비주얼 스튜디어는 이제 특정 이벤트 전후에 그런 스크립트들을 실행시키기 위한 기능을 빌트-인으로 지원한다. ASP.NET 프로젝트 템플릿은 *postrestore* 와 *prepare* 실행 중에 npm과 bower를 사용하는 클라이언트 단 종속성 (`client side dependencies`_)을 설치한다.

.. TODO add link to npm/bower article(s)

.. image:: understanding-aspnet5-apps/_static/scripts.png

The global.json File
--------------------

The global.json file is used to configure the solution as a whole. It includes just two sections, ``projects`` and ``sdk`` by default.

global.json 파일은 솔루션을 전체 하나로 구성할 때 쓰인다. 단지 두 개의 섹션만 존재하는데 ``prjects`` 와 ``sdk`` 이다.

.. literalinclude:: /../common/samples/WebApplication1/global.json
	:language: javascript

The *projects* property designates which folders contain source code for the solution. By default the project structure places source files in a *src* folder, allowing build artifacts to be placed in a sibling folder, making it easier to exclude such things from source control.

*projects* 속성은 어떤 폴더에 소스 코드가 존재하는지 알려준다. 기본적으로 프로젝트 구조상 *src* 폴더에서 소스 파일을 관리하고, 빌드 과정에서 생성되는 결과물은 *src* 폴더와 같은 수준의 폴더인 *artifacts* 에 넣음으로써 소스와 분리하고 있다. 

.. image:: understanding-aspnet5-apps/_static/solution-files.png

The *sdk* property specifies the version of the DNX (.Net Execution Environment) that Visual Studio will use when opening the solution. It's set here, rather than in project.json, to avoid scenarios where different projects within a solution are targeting different versions of the SDK.

*sdk* 속성은 DNX (.NET Excecution Environment)의 버전을 명시하고, 비주얼 스튜디오는 솔루션을 열면서 여기서 버전을 확인한다. 솔루션에 여러 프로젝트가 있다면 각각 다른 버전의 SDK 사용하는 것을 방지하기 위해 project.json 파일이 아닌 여기서 설정하고 있다.

.. _`the wwwroot folder` :

wwwroot
-------

In previous versions of ASP.NET, the root of the project was typically the root of the website. If you placed a *Default.aspx* file in the project root of an early version of ASP.NET, it would load if a request was made to the web application’s root. In later versions of ASP.NET, support for routing was added, making it possible to decouple the locations of files from their corresponding URLs (thus, HomeController in the Controllers folder is able to serve requests made to the root of the site, using a default route implementation). However, this routing  was used only for ASP.NET-specific application logic, not static files needed by the client to properly render the resulting page. Resources like images, script files, and stylesheets were generally still loaded based on their location within the file structure of the application, based off of the root of the project.

이전 버전의 ASP.NET 에서 프로젝트의 루트는 통상 웹 사이트의 루트였다. *Default.aspx* 파일을 이전 ASP.NET 프로젝트의 루트에 넣으면, 웹 애플리케이션의 루트를 향한 요청이 생겼을 때 로드되었다. 이후 버전의 ASP.NET 에서는 라우팅이 도입되면서 파일의 위치와 요청 URL의 관련성을 없앨 수 있었다(그래서, 기본 라우팅을 사용하여 HomeController가 사이트 루트에 대한 요청에 대응할 수 있다). 그러나, 이런 라우팅은 ASP.NET 애플리케이션 로직에만 사용되고 정적 파일들에는 사용할 수 없다. (여기 계속 완료)

.. image:: understanding-aspnet5-apps/_static/wwwroot.png

The file based approach presented several problems. First, protecting sensitive project files required framework-level protection of certain filenames or extensions, to prevent having things like *web.config* or *global.asax* served to a client in response to a request. Having to specifically block access (also know as blacklisting) to certain files is much less secure than granting access only to those files which should be accessible(also known as whitelisting). Typically different versions were required for dev/test and production (for example *web.config*).  Scripts would typically be referenced individually and in a readable format during development, but would be minified and bundled together when deployed for production. It’s beneficial to deploy only production files to production, but handling these kinds of scenarios was difficult with the previous file structure.

Enter the *wwwroot* folder in ASP.NET 5. The *wwwroot* folder represents the actual root of the web app when running on a web server. Static files, like *config.json*, which are not located in *wwwroot* will never be accessible, and there is no need to create special rules to block access to sensitive files. Instead of blacklisting access to sensitive files, a more secure whitelist approach is taken whereby only those files in the *wwwroot* folder are accessible via web requests.

In addition to the security benefits, the *wwwroot* folder also simplifies common tasks like bundling and minification, which can now be more easily incorporated into a standard build process and automated using tools like Grunt.

.. _`client side dependencies` :

Client Side Dependency Management
---------------------------------

The Dependencies folder contains two subfolders: Bower and NPM. These folders correspond to two package managers by the same names, and they’re used to pull in client-side dependencies and tools (e.g. jQuery, bootstrap, or grunt). Expanding the folders reveals which dependencies are currently managed by each tool, and the current version being used by the project.

.. image:: understanding-aspnet5-apps/_static/dependencies.png

The bower dependencies are controlled by the *bower.json* file. You'll notice that each of the items listed in the figure above correspond to dependencies listed in bower.json:

.. image:: understanding-aspnet5-apps/_static/bower-json.png

Each dependency is then further configured in its own section within the *bower.json* file, indicating how it should be deployed to the *wwwroot* folder when the bower task is executed.

By default, the bower task is executed using gulp, which is configured in *gulpfile.js*. The current web template’s gulpfile includes tasks for copying and cleaning script and CSS files from the bower folder to a ``/lib`` folder in ``wwwroot``.

.. image:: understanding-aspnet5-apps/_static/bower-npm-folders.png

.. _`server side dependencies` :

Server Side Dependency Management
---------------------------------

The *References* folder details the server-side references for the project. It should be familiar to ASP.NET developers, but it has been modified to differentiate between references for different framework targets, such as the full ASP.NET 5.0 vs. ASP.NET Core 5.0.  Within each framework target, you will find individual references, with icons indicating whether the reference is to an assembly, a NuGet package, or a project. Note that these dependencies are checked at compile time, with missing dependencies downloaded from the configured NuGet package source (specified under Options – NuGet Package Manager – Package Sources).	

.. image:: understanding-aspnet5-apps/_static/references.png

Configuring the Application
---------------------------

ASP.NET 5 no longer stores configuration settings in XML files (*web.config* and *machine.config*). Configuration is now stored in *config.json*, which was designed specifically for storing app configuration settings. The default ASP.NET project template includes Entity Framework, and so specifies the database connection string details in the *config.json* file included in the project.

.. image:: understanding-aspnet5-apps/_static/config-json.png

Individual entries within *config.json* are not limited to name-value pairs, but can specify rich objects. Entries can also reference other entries, as you can see the EF configuration does above.

There's nothing special about the *config.json* filename - it's specified by name in Startup.cs_. You can add as many different configuration files as makes sense for your app, rather than having to add to an ever-growing *web.config* file. You're also not limited to just JSON-formatted files - you can still use XML or even .INI files if you prefer.

Accessing configuration data from your app is best done by injecting the `IConfiguration <https://github.com/aspnet/Configuration/blob/dev/src/Microsoft.Framework.ConfigurationModel.Interfaces/IConfiguration.cs>`_ interface into your controller, and then simply calling its ``Get`` method with the name of the configuration element you need. For example, to store the application name in config and display it on the About page, you would need to make three changes to the default project. First, add the entry to *config.json*.

.. image:: understanding-aspnet5-apps/_static/add-config.png

Next, make sure ASP.NET knows what to return when a constructor requires an instance of ``IConfiguration``. In this case, we can specify that the configuration value is a singleton, since we don't expect it to change throughout the life of the application. We'll address *Startup.cs* in a moment, but for this step just add one line to the end of the ``ConfigureServices()`` method in *Startup.cs*:

.. code-block:: c#
	
	services.AddSingleton(_ => Configuration);

The third and final step is to specify that your controller expects an ``IConfiguration`` instance via its constructor. Following the `Explicit Dependencies Principle`_ with your classes is a good habit to get into, and will allow ASP.NET 5's built-in support for Dependency Injection to work correctly. Assign the instance to a local field, and then access the configuration value by calling the ``Get`` method on this instance.

.. _`Explicit Dependencies Principle`: http://deviq.com/explicit-dependencies-principle/

You will need to ensure you have this using statement:

.. code-block:: c#

	using Microsoft.Framework.ConfigurationModel;
	
Then, update the controller as shown:

.. image:: understanding-aspnet5-apps/_static/get-config.png

Run the application and navigate to the About page and you should see the result.

.. image:: understanding-aspnet5-apps/_static/about-page.png

.. _Startup.cs: 
.. _fundamentalconcepts-application-startup:

Application Startup
-------------------

ASP.NET 5 has decomposed its feature set into a variety of modules that can be individually added to a web app. This allows for lean web apps that do not import or bring in features they don't use. When your ASP.NET app starts, the ASP.NET runtime calls ``Configure`` in the ``Startup`` class. If you create a new ASP.NET web project using the Empty template, you will find that the *Startup.cs* file has only a couple lines of code. The default Web project’s ``Startup`` class wires up configuration, MVC, EF, Identity services, logging, routes, and more. It provides a good example for how to configure the services used by your ASP.NET app. There are three parts to the sample startup class: a constructor, ``ConfigureServices``, and ``Configure``. The ``Configure`` method is called after ``ConfigureServices`` and is used to configure middleware.

The constructor specifies how configuration will be handled by the app. Configuration is a property of the ``Startup`` class and can be read from a variety of file formats as well as from environment variables. The default project template wires up ``Configuration`` to use a *config.json* and environment variables.

.. code-block:: c#

	public Startup(IHostingEnvironment env)
	{
		// Setup configuration sources.
		Configuration = new Configuration()
			.AddJsonFile("config.json")
			.AddEnvironmentVariables();
	}
	
The ``ConfigureServices`` method is used to specify which services are available to the app. The default template uses helper methods to add a variety of services used for EF, Identity, and MVC. This is also where you can add your own services, as we did above to expose the configuration as a service. The complete ``ConfigureServices`` method, including the call to add ``Configuration`` as a singleton, is shown here:

.. code-block:: c#

	// This method gets called by the runtime.
	public void ConfigureServices(IServiceCollection services)
	{
		// Add EF services to the services container.
		services.AddEntityFramework(Configuration)
			.AddSqlServer()
			.AddDbContext<ApplicationDbContext>();

		// Add Identity services to the services container.
		services.AddIdentity<ApplicationUser, IdentityRole>(Configuration)
			.AddEntityFrameworkStores<ApplicationDbContext>();

		// Add MVC services to the services container.
		services.AddMvc();

		services.AddSingleton(_ => Configuration);
	}
	
Finally, the ``Configure`` method will be called by the runtime after ``ConfigureServices``. In the sample project, ``Configure`` is used to wire up a console logger, add several useful features for the development environment, add support for static files, Identity, and MVC routing. Note that adding Identity and MVC in ``ConfigureServices`` isn’t sufficient - they also need to be configured in  the request pipeline via these calls in ``Configure``.

.. code-block:: c#

	// Configure is called after ConfigureServices is called.
	public void Configure(IApplicationBuilder app, IHostingEnvironment env, ILoggerFactory loggerfactory)
	{
		// Configure the HTTP request pipeline.
		// Add the console logger.
		loggerfactory.AddConsole();

		// Add the following to the request pipeline only in development environment.
		if (string.Equals(env.EnvironmentName, "Development", StringComparison.OrdinalIgnoreCase))
		{
			app.UseBrowserLink();
			app.UseErrorPage(ErrorPageOptions.ShowAll);
			app.UseDatabaseErrorPage(DatabaseErrorPageOptions.ShowAll);
		}
		else
		{
			// Add Error handling middleware which catches all application specific errors and
			// send the request to the following path or controller action.
			app.UseErrorHandler("/Home/Error");
		}

		// Add static files to the request pipeline.
		app.UseStaticFiles();

		// Add cookie-based authentication to the request pipeline.
		app.UseIdentity();

		// Add MVC to the request pipeline.
		app.UseMvc(routes =>
		{
			routes.MapRoute(
				name: "default",
				template: "{controller}/{action}/{id?}",
				defaults: new { controller = "Home", action = "Index" });
		});
	}

As you can see, configuring which services are available and how the request pipeline is configured is now done completely in code in the ``Startup`` class, as opposed to using HTTP Modules and Handlers managed via *web.config*. 

.. TODO: You can learn more about how the request pipeline is configured as well as how to write your own middleware components.
	
Summary
-------

ASP.NET 5 introduces a few concepts that didn't exist in previous versions of ASP.NET. Rather than working with *web.config*, packages.config, and a variety of project properties stored in the .csproj/.vbproj file, developers can now work with specific files and folders devoted to specific purposes. Although at first there is some learning curve, the end result is more secure, more maintainable, works better with source control, and has better separation of concerns than the approach used in previous versions of ASP.NET.

