.. _dnx-overview:

DNX 소개
========

By `Daniel Roth`_

What is the .NET Execution Environment?
---------------------------------------------

The .NET Execution Environment (DNX) is a software development kit (SDK) and runtime environment that has everything you need to build and run .NET applications for Windows, Mac and Linux. It provides a host process, CLR hosting logic and managed entry point discovery.  DNX was built for running cross-platform ASP.NET Web applications, but it can run other types of .NET applications, too, such as cross-platform console apps.

닷넷 실행 환경(DNX - .NET Execution Environment)은 소프트웨어 개발 도구(SDK - Software Development Kit)이면서 윈도우, 맥, 리눅스에서 운영할 닷넷 애플리케이션을 작성하는데 필요한 모든 것을 제공하는 런타임이다. DNX는 호스트 프로세스, CLR을 호스팅하는 로직을 갖고 있고 호스팅하는 애플리케이션의 진입점을 찾을 수 있다. DNX는 크로스플랫폼에서 동작하는 ASP.NET 웹 애플리케이션을 위해 작성되었지만 또한 콘솔 앱과 같은 다른 종류의 닷넷 애플리케이션들을 운영할 수도 있다. 

Why build DNX?
--------------

**Cross-platform .NET development** DNX provides a consistent development and execution environment across multiple platforms (Windows, Mac and Linux) and across different .NET flavors (.NET Framework, .NET Core and Mono).
With DNX you can develop your application on one platform and run it on a different platform as long as you have a compatible DNX installed on that platform. You can also contribute to DNX projects using your development platform and tools of choice.

**크로스 플랫폼 닷넷 개발** - DNX는 윈도우, 맥, 리눅스를 아우르는 크로스플랫폼을 지원하면서 닷넷 프레임워크, 닷넷 코어, Mono를 아우르는 선택적인 개발 환경을 수용할 수 있는 런타임으로써 일관적인 개발을 가능하게 해준다. DNX의 존재 때문에 맥에서 애플리케이션을 개발하고 리눅스에서 운영할 수 있게 되었다. 물론, 개발과 운영, 두 개의 플랫폼은 서로 호환 가능한 DNX가 설치되어 있어야 할 것이다. 또한, 여러분의 개발 플랫폼과 개발 툴을 DNX 프로젝트에 기여할 수도 있다.  

**Build for .NET Core** DNX dramatically simplifies the work needed to develop cross-platform applications using .NET Core. It takes care of hosting the CLR, handling dependencies and bootstrapping your application. You can easily define projects and solutions using a lightweight JSON format (*project.json*), build your projects and publish them for distribution.

**닷넷 코어용 빌드** - DNX는 닷넷 코어를 사용하여 크로스플랫폼 개발에 필요한 작업을 드라마틱하게 간소화해준다. DNX는 CLR을 호스팅하고 애플리케이션의 종속성을 처리하면서 여러분의 애플리케이션을 구동한다. 경량화된 JSON 형식의 *project.json* 파일을 사용하여 아주 쉽게 프로젝트와 솔루션을 정의할 수 있다. 이 파일을 통해 프로젝트들을 빌드하고 배포할 수 있다.

**Package ecosystem** Package managers have completely changed the face of modern software development and DNX makes it easy to create and consume packages. DNX provides tools for installing, creating and managing NuGet packages. DNX projects simplify building NuGet packages by cross-compiling for multiple target frameworks and can output NuGet packages directly. You can reference NuGet packages directly from your projects and transitive dependencies are handled for you. You can also build and install development tools as packages for your project and globally on a machine.

**패키지 생태계**  - 패키지 관리자는 모던 소프트웨어의 한 면을 완벽히 바꿨다. DNX 역시 패키지 관리자를 사용하여 패키지들을 쉽게 생성하고 사용할 수 있게 해준다. DNX가 제공하는 도구(tools)들은 NuGet 패키지를 설치, 생성, 관리한다. DNX 프로젝트는 멀티 타겟 프레임워크에 대한 크로스 컴파일을 수행함으로써 NuGet 패키지 작성을 간단하게 만들어 준다. 여러분의 프로젝트에서 패키지를 직접 참조할 수 있고, 패키지가 의존하는 다른 종속성은 자동으로 처리된다. 여러분은 또한 프로젝트 개발에 필요한 도구들을 패키지로 직접 작성하여 필요한 프로젝트에 설치할 수 있다, 또한 서버에 설치하여 글로벌하게 사용할 수도 있다. 

**Open source friendly** DNX makes it easy to work with open source projects. With DNX projects you can easily replace an existing dependency with its source code and let DNX compile it in-memory at runtime. You can then debug the source and modify it without having to modify the rest of your application.

**오픈소스 친화적** - DNX는 오픈소스 프로젝트의 작업을 쉽게해 준다. DNX 프로젝트에서는 기존 종속성을 쉽게 소스 코드로 대치하여 DNX가 런타임시 인메모리 컴파일하게 할 수 있다. 이 덕에, 소스를 디버그할 수 있고 애플리케이션의 다른 부분을 변경하지 않고 소스를 변경할 수 있다.

.. _dnx-concept-projects:

Projects
--------

A DNX project is a folder with a *project.json* file. The name of the project is the folder name. You use DNX projects to build NuGet packages. The *project.json* file defines your package metadata, your project dependencies and which frameworks you want to build for:

DNX 프로젝트는 *project.json* 파일이 있는 폴더라고 할 수 있다. 폴더명이 곧 프로젝트명이다. DNX 프로젝트를 이용해서 NuGet 패키지를 만든다. *project.json* 파일은 어떤 종속성을 갖는지 어떤 프레임워크를 대상으로 하는지 설명하는 메타데이터를 정의한다. 

.. literalinclude:: /../common/samples/ClassLibrary1/src/ClassLibrary1/project.json
  :linenos:
  :language: json

All the files in the folder are by default part of the project unless explicitly excluded in *project.json*.

폴더내의 모든 파일은 *project.json* 에서 명시적으로 제외처리하지 않는한 기본적으로 프로젝트의 일부이다.  

You can also define commands as part of your project that can be executed (see :ref:`dnx-concept-commands`).

또한 외부에서 실행할 수 있는 명령어도 정의할 수 있다 (:ref:`dnx-concept-commands` 참조).

You specify which frameworks you want to build for under the "frameworks" property. DNX will cross-compile for each specified framework and create the corresponding lib folder in the built NuGet package.

"frameworks" 속성내에 어떤 프레임워크들을 사용할지 명시한다. DNX는 명시된 각 프레임워크에 대한 크로스컴파일을 하고 해당 lib 폴더를 작성된 NuGet 패키지에 생성한다.

You can use the .NET Development Utility (DNU) to build, package and publish DNX projects. Building a project produces the binary outputs for the project. Packaging produces a NuGet package that can be uploaded to a package feed (for example, http://nuget.org) and then consumed. Publishing collects all required runtime artifacts (the required DNX and packages) into a single folder so that it can be deployed as an application.

DNU(.NET Development Utility)를 사용하여 DNX 프로젝트를 빌드, 패키지, 퍼블리쉬할 수 있다. 프로젝트를 빌드하면 바이너리 결과를 만들어낸다. 패키지한다는 것은 하나의 NuGet 패키지를 만든다는 의미이고 이렇게 만든 패키지는 http://nuget.org 와 같은 패키지 제공 사이트에 업로드해서 다른 사람들이 사용할 수 있도록 한다. 퍼플리쉬는 애플리케이션 운영에 필요한 DNX와 종속성으로 정의된 모든 패키지들을 하나의 폴더에 수집하여 그 폴더를 애플리케이션으로서 배포하는 것이다.  

For more details on working with DNX projects see :doc:`/dnx/projects`.

DNX 프로젝트를 다루는 보다 자세한 내용은 :doc:`/dnx/projects` 을 참고하자.

.. _dnx-concept-dependencies:

Dependencies
-------------------

Dependencies in DNX consist of a name and a version number. Version numbers should follow `Semantic Versioning <http://semver.org>`_. Typically dependencies refer to an installed NuGet package or to another DNX project. Project references are resolved using peer folders to the current project or  project paths specified using a *global.json* file at the solution level:

DNX에서 종속성은 이름과 버전 넘버로 구성된다. 버전 넘버는 Semantic Versioning (`유의적 버전 <http://semver.org/lang/ko/>`_) 규칙을 지켜야 한다. 종속성은 NuGet 패키지를 참조하거나 다른 DNX 프로젝트를 참고하는 것이 전형적인 구성이다. 프로젝트간의 참조는 프로젝트 폴더와 같은 레벨에 존재하는 프로젝트명의 폴더를 찾아 보거나, 솔루션 레벨에서 설정하고 있는 *global.json* 파일의 projects 속성에 설정된 경로를 참고한다.

.. literalinclude:: /../common/samples/ClassLibrary1/global.json
  :linenos:
  :language: json

The *global.json* file also defines the minimum DNX version ("sdk" version) needed to build the project.

*global.json* 파일은 또한 프로젝트를 빌드하기 위한 최저 DNX 버전 ("sdk" version)을 정의한다.

Dependencies are transitive in that you only need to specify your top level dependencies. DNX will handle resolving the entire dependency graph for you using the installed NuGet packages. Project references are resolved at runtime by building the referenced project in memory. This means you have the full flexibility to deploy your DNX application as package binaries or as source code.

종속성은 다른 패키지에 종속성을 갖을 수 있지만 여러분은 사용하고자 하는 톱 레벨의 종속성만 명시하면 된다. DNX가 설치된 톱 레벨의 NuGet 패키지를 분석한 후, 전체 종속성 그래프를 파악해서 나머지 작업을 처리할 것이다. 프로젝트 참조는 실행 시점에서 참조된 프로젝트를 메모리 상에 빌드하는 것으로 해결된다. 이렇게 DNX가 의존하는 패키지와 프로젝트를 자동으로 처리해 주기 때문에 개발자의 입장에서는, DNX 애플리케이션을 패키지 바이너리로 배포하던 소스 코드로 배포하던, 배포상의 엄청난 유연성을 갖게 되는 것이다.

.. _dnx-concept-packages-and-feeds:

Packages and feeds
---------------------------

For package dependencies to resolve they must first be installed. You can use DNU to install a new package into an existing project or to restore all package dependencies for an existing project. The following command downloads and installs all packages that are listed in the *project.json* file::

패키지 종속성을 해결하기 위해서는 일단 설치가 되어야 한다. DNU을 사용하여 새 패키지를 프로젝트에 설치할 수도 있고, 기존 프로젝트 상의 모든 패키지 복구할 수도 있다. 다음의 명령문은 *project.json* 파일에 정의된 모든 패키지들을 다운로드하여 설치하기 위해 사용한다.

    dnu restore

Packages are restored using the configured set of package feeds. You configure the available package feeds using `NuGet configuration files (NuGet.config) <http://docs.nuget.org/consume/nuget-config-file>`_.

패키지들은 패키지 피드라고 설정 모음을 통해 복구된다. `NuGet configuration files (NuGet.config) <http://docs.nuget.org/consume/nuget-config-file>`_ 를 이용하여 패키지 피드를 구성할 수 있다.

.. _dnx-concept-commands:

Commands
--------

A command is a named execution of a .NET entry point with specific arguments. You can define commands in your *project.json* file:

커맨드는 특정 인자를 갖는 닷넷 시작점에 대한 실행명(named execution)이다. *project.json* 파일에 커맨드를 정의할 수 있다.

.. literalinclude:: /../common/samples/WebApplication1/src/WebApplication1/project.json
  :linenos:
  :language: json
  :lines: 31-34
  :dedent: 2

You can then use DNX to execute the commands defined by your project, like this::

프로젝트에 정의한 커맨드를 실행하기 위해 DNX를 사용할 수 있다. ::

    dnx . web

Commands can  be built and distributed as NuGet packages. You can then use DNU to install commands globally on a machine::

커맨드들만 빌드되어 NuGet 패키지로 배포될 수도 있다. 이런 커맨드들을 머신에 글로벌하게 설치하기 위해 DNU를 사용할 수 있다. ::

    dnu commands install MyCommand

For more information on using and creating commands see :doc:`/dnx/commands`.

커맨드를 생성하고 사용하기 위한 자세한 정보는 :doc:`/dnx/commands` 를 참조하자.

.. _dnx-concept-apphost:

Application Host
----------------

The DNX application host is typically the first managed entry point invoked by DNX and is responsible for handling dependency resolution, parsing *project.json*, providing additional services and invoking the application entry point.

(역주: 이 부분의 설명이 다소 어렵다면 `DNX Structure <https://github.com/aspnet/Home/wiki/DNX-structure>`_ 라는 글을 먼저 읽어 보는 것도 좋은 방법이다)

DNX의 애플리케이션 호스트라는 것은 DNX의 전체 구조상 관리영역(CLR 위에서 동작하는 managed 영역)에 위치하면서 DNX에 의해 호출되는 컴포넌트다. 애플리케이션 호스트는 종속성을 풀어내고, *project.json* 파일을 파싱하고, 추가적인 서비스를 제공하고 애플리케이션의 시작점을 찾아 구동하는 책임을 갖는다.

Alternatively, you can have DNX invoke your application's entry point directly. Doing so requires that your application be fully built and all dependencies located in a single directory. Using DNX without using the DNX Application Host is not common.

애플리케이션 호스트를 거치지 않고 DNX가 직접 애플리케이션을 호출하는 다른 방법도 있다. 이 방법은 애플리케이션이 완벽히 빌드되어 있고 모든 종속성이 단일 디렉토리에 위치해 있어야 가능하다. 애플리케이션 호스트를 사용하지 않고 DNX를 쓴다는 것은 일반적이라고 할 수 없다. 

The DNX application host provides a set of services to applications through dependency injection (for example, `IServiceProvider`, `IApplicationEnvironment` and `ILoggerFactory`). Application host services can be injected in the constructor of the class for your `Main` entry point or as additional method parameters to your `Main` entry point.

DNX 애플리케이션 호스트는 종속성 주입을 통해 애플리케이션에 여러 가지 서비스를 제공한다. `IServiceProvider`, `IApplicationEnvironment`, `ILoggerFactory` 와 같은 서비스들이 그 예다. 애플리케이션 호스트 서비스들은 `Main` 시작점의 클래스 생성자에서 또는 `Main` 시작점의 추가적인 매개변수로 주입될 수 있다.

.. _dnx-concept-compile-modules:

Compile Modules
---------------

Compile modules are an extensibility point that let you participate in the DNX compilation process. You implement a compile module by implementing the `ICompileModule <https://github.com/aspnet/dnx/blob/dev/src/Microsoft.Dnx.Compilation.CSharp.Abstractions/ICompileModule.cs>`_ interface and putting your compile module in a compiler/preprocess or compiler/postprocess in your project.

컴파일 모듈은 여러분이 DNX의 컴파일 과정에 참여할 수 있게 해주는 확장 포인트이다. `ICompileModule <https://github.com/aspnet/dnx/blob/dev/src/Microsoft.Dnx.Compilation.CSharp.Abstractions/ICompileModule.cs>`_ 인터페이스를 구현하는 것으로 컴파일 모듈을 만들어 compiler/preprocess 또는 compiler/postprocess에 삽입하면 된다.

DNX Version Manager
-------------------

You can install multiple DNX versions and flavors on your machine. To install and manage different DNX versions and flavors you use the .NET Version Manager (DNVM). DNVM lets you list the different DNX versions and flavors on your machine, install new ones and switch the active DNX.

See :doc:`/getting-started/index` for instructions on how to acquire and install DNVM for your platform.

다른 종류, 다른 버전의 DNX를 설치할 수 있다. 이렇게 다른 DNX 들을 설치하고 관리하기 위해서는 .NET Version Manager (DNVM)를 사용한다. DNVM을 통해 모든 DNX의 목록을 확인하고 액티브 DNX를 지정할 수 있다.

여러분의 플랫폼에 맞는 DNVM을 찾고 설치하는 것에 대한 자세한 내용은 :doc:`/getting-started/index` 글을 참조하자.