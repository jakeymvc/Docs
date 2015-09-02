ASP.NET 5 소개
=============

By `Daniel Roth`_

ASP.NET 5 is a significant redesign of ASP.NET. This topic introduces the new concepts in ASP.NET 5 and explains how they help you develop modern web apps.

ASP.NET 5를 설계 관점에서 한 마디로 설명하자면 ASP.NET의 심각한 재설계(significant redesign)라고 할 수 있다. 이번 주제는 ASP.NET 5 내의 새로운 개념을 소개하고 그 것들이 어떻게 현대적인 웹 앱을 개발하는데 도움이 되는지 설명하고자 한다.

What is ASP.NET 5?
------------------

ASP.NET 5 is a new open-source and cross-platform framework for building modern cloud-based Web applications using .NET. We built it from the ground up to provide an optimized development framework for apps that are either deployed to the cloud or run on-premises. It consists of modular components with minimal overhead, so you retain flexibility while constructing your solutions. You can develop and run your ASP.NET 5 applications cross-platform on Windows, Mac and Linux. ASP.NET 5 is fully open source on `GitHub <https://github.com/aspnet/home>`_.

ASP.NET 5는 닷넷을 사용하여 현대적인 클라우드 기반의 웹 애플리케이션을 만들기 위한 새로운 오픈소스이자 크로스-플랫폼 프레임워크다. 우리는 클라우드에 배포되거나 자체 호스팅 서버(on-premise)에서 동작하는 앱을 위한 최적의 개발 프레임워크를 제공하기 위해 프레임워크를 바닥부터 다시 만들었다. ASP.NET 5는 최소한의 오버헤드만으로 모듈화된 컴포넌트들로 구성되어 있기 때문에 솔루션을 구성하면서 유연성을 유지할 수 있다. 뿐만아니라, 여러분은 ASP.NET 5 애플리이션을 윈도우, 맥, 리눅스에서 개발하고 실행할 수 있다. ASP.NET 5는 `GitHub <https://github.com/aspnet/home>`_ 의 오픈 소스이다.

Why build ASP.NET 5?
--------------------

The first preview release of ASP.NET 1.0 came out almost 15 years ago.  Since then millions of developers have used it to build and run great web applications, and over the years we have added and evolved many, many capabilities to it.

ASP.NET 1.O의 최초 프리뷰가 나온 것이 어느 덧 15년 전의 일이다. 그 이래로 정말 많은 개발자들이 ASP.NET을 사용하여 훌륭한 웹 애플리케이션을 만들어 왔고 우리는 그 동안 수 많은 기능들을 추가하고 발전시켜왔다.

With ASP.NET 5 we are making a number of architectural changes that make the core web framework much leaner and more modular. ASP.NET 5 is no longer based on System.Web.dll, but is instead based on a set of granular and well factored NuGet packages allowing you to optimize your app to have just what you need. You can reduce the surface area of your application to improve security, reduce your servicing burden and also to improve performance in a true pay-for-what-you-use model.

ASP.NET 5에서 우리는 꽤 많은 아키텍쳐 변경을 통해 군더더기 없이 모듈화된 코어(core) 웹 프레임워크를 만들고 있다. ASP.NET 5는 System.Web.dll 을 과감히 버리고 대신, 잘게 요소화된 NuGet 패키지들에 기반해서 여러분의 요구에 최적화된 앱을 만들 수 있게 해준다. 이렇게 사용한 만큼 지불하는(pay-for-what-you-use) 모델을 채택함으로써 애플리케이션에서 외부로 노출되는 것들이 줄어들어 보안 측면에서 개선을 기할 수 있고, 서비스 하는 부담 또한 줄어들어 성능면에서 개선효과를 볼 수 있다.

ASP.NET 5 is built with the needs of modern Web applications in mind, including a unified story for building Web UI and Web APIs that integrate with today's modern client-side frameworks and development workflows. ASP.NET 5 is also built to be cloud-ready by introducing environment-based configuration and by providing built-in dependency injection support.

ASP.NET 5는 현대적인 웹 애플리케이션에 대한 필요를 염두에 두고 만들어졌다. 웹 사용자 인터페이스를 만드는 것, 클라이언트 측 프레임워크와 통합되는 Web API들을 만드는 것, 이런 개발 작업의 흐름이 하나의 통일된 스토리가 된다. ASP.NET 5는 또한 클라우드 준비된(cloud-ready) 프레임워크라고 할 수 있다. 환경 기반의 구성(environment-based configuration)을 도입하고, 빌트-인 종속성 주입(dependency injection)을 제공하기 때문이다.

To appeal to a broader audience of developers, ASP.NET 5 supports cross-platform development on Windows, Mac and Linux. The entire ASP.NET 5 stack is open source and encourages community contributions and engagement. ASP.NET 5  comes with a new, agile project system in Visual Studio while also providing a complete command-line interface so that you can develop using the tools of your choice.

보다 광범위한 개발자들의 관심을 끌기 위해, ASP.NET 5는 윈도우, 맥, 리눅스에서 크로스-플랫폼 개발을 지원한다. 전체 ASP.NET 5 스택은 오픈 소스이고 커뮤니티의 기여와 참여를 장려하고 있다. 비주얼 스튜디오는 완벽한 커맨드-라인 인터페이스도 지원하면서도 새로운 애자일 프로젝트 시스템을 도입했다. 그 덕에 여러분이 선택한 툴을 사용해서 개발할 수 있게 되었다.

In summary, with ASP.NET 5 you gain the following foundational improvements:

정리하자면, 여러분은 ASP.NET 5에서 아래의 기초적인 개선사항들을 얻게 되었다.

- New light-weight and modular HTTP request pipeline
- Ability to host on IIS or self-host in your own process
- Built on .NET Core, which supports true side-by-side app versioning
- Ships entirely as NuGet packages
- Integrated support for creating and using NuGet packages
- Single aligned web stack for Web UI and Web APIs
- Cloud-ready environment-based configuration
- Built-in support for dependency injection
- New tooling that simplifies modern web development
- Build and run cross-platform ASP.NET apps on Windows, Mac and Linux
- Open source and community focused

* 새롭게 경량화되고 모듈화된 HTTP 요청 파이프라인
* IIS 또는 여러분 자신의 프로세스에서 셀프 호스트할 수 있는 능력
* 닷넷 코어에 기반한 진정한 sidy-by-side 앱 버전 관리(versioning)
* 모든 기능이 NuGet 패키지 형태로 추가
* NuGet 패키지들을 생성하고 사용하는 것에 대한 통합된 지원
* 웹 사용자 인터페이스와 웹 API를 위한 단일 웹 스택
* 클라우드 준비된 환경 기반의 구성
* 빌트-인 종속성 주입 기능
* 현대적인 웹 개발을 단순화 시킨 새로운 툴링(tooling)
* 윈도우, 맥, 리눅스에서 개발하고 실행할 수 있는 크로스-플랫폼
* 오픈 소스와 커뮤니티 중심

Application anatomy
-------------------

ASP.NET 5 applications are built and run using the new :doc:`.NET Execution Environment (DNX) </dnx/overview>`. Every ASP.NET 5 project is a :doc:`DNX project </dnx/projects>`. ASP.NET 5 integrates with DNX through the `ASP.NET Application Hosting <https://nuget.org/packages/Microsoft.AspNet.Hosting>`_ package.

ASP.NET 5 애플리케이션은 새로운 :doc:`.NET Execution Environment (DNX) </dnx/overview>` 를 사용하여 작성되고 실행된다. 모든 ASP.NET 5 프로젝트는 곧 :doc:`DNX project </dnx/projects>` 프로젝트이며 `ASP.NET Application Hosting <https://nuget.org/packages/Microsoft.AspNet.Hosting>`_ 패키지를 사용하여 통합된다.

ASP.NET 5 applications are defined using a public ``Startup`` class:

ASP.NET 5 애플리케이션은 ``Startup`` 클래스를 사용하여 정의된다.

.. code-block:: c#

    public class Startup
    {
         public void ConfigureServices(IServiceCollection services)
         {
         }

         public void Configure(IApplicationBuilder app)
         {
         }
    }

The ``ConfigureServices`` method defines the services used by your application and the ``Configure`` method is used to define what middleware makes up your request pipeline. See :doc:`understanding-aspnet5-apps` for more details.

``ConfigureServices`` 메서드는 애플리케이션에 사용될 서비스들을 정의하고 ``Configure`` 메서드는 요청 파이프라인을 구성할 미들웨어를 정의하는데 사용된다. 보다 자세한 사항은 :doc:`understanding-aspnet5-apps` 아티클을 참조하자.

Services
--------

A service is a component that is intended for common consumption in an application. Services are made available through dependency injection. ASP.NET 5 includes a simple built-in inversion of control (IoC) container that supports constructor injection by default, but can be easily replaced with your IoC container of choice. See :doc:`/fundamentals/dependency-injection` for more details.

서비스는 애플리케이션에서 공통적으로 사용하고자 하는 목적의 컴포넌트다. 서비스들은 종속성 주입을 통해 사용이 가능하다. ASP.NET 5 는 간단한 빌트-인 제어 역전 (IoC) 컨테이너를 포함하고 있는데 생성자를 이용한 주입 방식을 기본으로 지원하고 있다. 그러나, 여러분이 사용하는 IoC 컨테이너로 쉽게 대체할 수도 있다. 자세한 내용은 :doc:`/fundamentals/dependency-injection` 아티클을 참조하자.

Services in ASP.NET 5 come in three varieties: singleton, scoped and transient. Transient services are created each time they’re requested from the container. Scoped services are created only if they don’t already exist in the current scope. For Web applications, a container scope is created for each request, so you can think of scoped services as per request. Singleton services are only ever created once.

ASP.NET 5 에서 서비스는 세 가지 종류(singleton, scoped, transient)로 구분된다. Transient 서비스는 컨테이너로부터 요청될 때마다 생성되고 Scoped 서비스는 현재 scope에 서비스가 존재하지 않을 때만 서비스를 생성한다. 웹 애플리케이션에서 컨테이너의 범주는 매 요청에 해당하므로 scoped 서비스는 요청 당 서비스로 생각할 수 있다. 반면, Singleton 서비스는 오직 한번만 생성된다.

Middleware
----------

In ASP.NET 5 you compose your request pipeline using :doc:`/fundamentals/middleware`. ASP.NET 5 middleware perform asynchronous logic on an ``HttpContext`` and then optionally  invoke the next middleware in the sequence or terminate the request directly. You generally "Use" middleware by invoking a corresponding extension method on the ``IApplicationBuilder`` in your ``Configure`` method.

ASP.NET 5 에서는 :doc:`/fundamentals/middleware` 를 사용하여 요청 파이프라인을 구성한다. ASP.NET 5 미들웨어는 ``HttpContext`` 에 대해 비동기 로직을 수행하고 선택적으로 다음 미들웨어를 호출하거나 요청 처리 작업을 중단한다. 일반적으로 미들웨어에 대응하는 ``IApplicationBuilder`` 의 확장 메서드를 ``Configure`` 메서드에서 호출하는 것으로 요청 파이프라인을 작성한다.

ASP.NET 5 comes with a rich set of prebuilt middleware:

ASP.NET 5 는 미리 작성된 풍부한 미들웨어를 제공한다. 아래는 그 중 일부이다.

- :doc:`/fundamentals/static-files`
- :doc:`/fundamentals/routing`
- :doc:`/fundamentals/diagnostics`
- :doc:`Authentication </security/index>`

You can also author your own :doc:`custom middleware </fundamentals/middleware>`.

You can use any `OWIN <http://owin.org>`_-based middleware with ASP.NET 5. See :doc:`/fundamentals/owin` for details.

여러분은 여러분만의 :doc:`custom middleware </fundamentals/middleware>` 를 작성할 수도 있고 `OWIN <http://owin.org>`_ 기반의 미들웨어를 작성할 수도 있는데 OWIN과 관련하여 자세한 내용은 :doc:`/fundamentals/owin` 아티클을 참조하자.

Servers
-------

The ASP.NET Application Hosting model does not directly listen for requests, but instead relies on an HTTP server implementation to surface the request to the application as a set of feature interfaces that can be composed into an HttpContext.

ASP.NET 애플리케이션 호스팅 모델은 요청을 직접 리스닝하지 않는다. 그 대신, HTTP 서버 구현에 의지하여 애플리케이션에 대한 요청을 (HttpContext 와 작용하는 기능적인 인터페이스들의 모음으로서) 표면화한다.

ASP.NET 5 includes server support for running on IIS or self-hosting in your own process. On Windows you can host your application outside of IIS using the `WebListener <https://nuget.org/packages/Microsoft.AspNet.Server.WebListener>`_ server, which is based on HTTP.sys. You can also host your application on a non-Windows environment using the cross-platform `Kestrel <https://nuget.org/packages/Kestrel>`_ web server.

ASP.NET 5 는 IIS에서 운영하거나 자신의 프로세스에서 셀프 호스팅하는 서버를 지원한다. 윈도우에서는 HTTP.sys 에 기반한 `WebListener <https://nuget.org/packages/Microsoft.AspNet.Server.WebListener>`_ 를 통해 IIS 밖에서 애플리케이션을 호스팅할 수 있다. 또한, 비 윈도우 환경에서도 크로스-플랫폼 `Kestrel <https://nuget.org/packages/Kestrel>`_ 웹 서버를 사용하여 여러분의 애플리케이션을 호스팅할 수 있다.


Web root
--------

The Web root of your application is the root location in your project from which HTTP requests are handled (ex. handling of static file requests). The Web root of an ASP.NET 5 application is configured using the "webroot" property in your project.json file.

애플리케이션의 웹 루트는 프로젝트의 루트라고 할 수 있다. 이 곳으로부터 예를 들면, 정적 파일에 대한 접근 시도 같은 HTTP 요청이 처리된다. ASP.NET 5 애플리케이션의 웹 루트는 project.json 파일의 “webroot” 속성을 사용하여 설정된다.

Configuration
-------------

ASP.NET 5 uses a new configuration model for handling of simple name-value pairs that is not based on System.Configuration or web.config. This new configuration model pulls from an ordered set of configuration providers. The built-in configuration providers support a variety of file formats (XML, JSON, INI) and also environment variables to enable environment-based configuration. You can also write your own custom configuration providers. Environments, like Development and Production, are a first-class notion in ASP.NET 5 and can also be set up using environment variables:

ASP.NET 5는 간단한 이름-값 쌍을 다루는 새로운 구성모델을 사용하며 이 새 모델은 System.Configuration 또는 web.config 에 기반하지 않는다. 새 구성 모델은 구성 제공자(configuration provider)의 순차적인 집합에서 정보를 얻는다. 빌트-인 구성 제공자는 XML, JSON, INI 파일등 다양한 파일 형식을 지원하며 또한, 환경 기반의 구성을 가능케 하는 환경 변수도 지원한다. 여러분은 이와 더불어 사용자 정의 구성 제공자를 작성할 수도 있다. 개발환경, 운영환경 처럼 환경이 ASP.NET 5에서는 최고의 개념이고 환경 변수를 통해 설정될 수도 있다.


.. code-block:: c#

    // Setup configuration sources.
    var configuration = new Configuration()
        .AddJsonFile("config.json")
        .AddJsonFile($"config.{env.EnvironmentName}.json", optional: true);

    if (env.IsEnvironment("Development"))
    {
        // This reads the configuration keys from the secret store.
        // For more details on using the user secret store see http://go.microsoft.com/fwlink/?LinkID=532709
        configuration.AddUserSecrets();
    }
    configuration.AddEnvironmentVariables();
    Configuration = configuration;

See :doc:`/fundamentals/configuration` for more details on the new configuration system and :doc:`/fundamentals/environments` for details on how to work with environments in ASP.NET 5.

새로운 구성모델에 대한 자세한 내용은 :doc:`/fundamentals/configuration` 아티클을 참조하고 ASP.NET 5에서 환경과 관련된 작업에 대한 자세한 내용은 :doc:`/fundamentals/environments` 아티클을 참조하자.


Client-side development
-----------------------

ASP.NET 5 is designed to integrate seamlessly with a variety of client-side frameworks, including `AngularJS <https://angularjs.org/>`_, `KnockoutJS <http://knockoutjs.com>`_ and `Bootstrap <http://getbootstrap.com/>`_. See :doc:`/client-side/index` for more details.

ASP.NET 5는 클라이언트 측 프레임워크와 매끄럽게 통합되도록 설계되었고 `AngularJS <https://angularjs.org/>`_ , `KnockoutJS <http://knockoutjs.com>`_ and `Bootstrap <http://getbootstrap.com/>`_ 와 같은 프레임워크를 포함한다. 이와 관련하여 자세한 내용은 :doc:`/client-side/index` 아티클을 참조하자.


