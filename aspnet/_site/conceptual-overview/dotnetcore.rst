닷넷 코어 소개
=============

By `Steve Smith`_ 

.NET Core is a small, optimized runtime that can be targeted by ASP.NET 5 applications. In fact, the new ASP.NET 5 project templates target .NET Core by default, in addition to the .NET Framework. Learn what targeting .NET Core means for your ASP.NET 5 application.

닷넷 코어는 ASP.NET 5 애플리케이션에서 사용할 수 있는 작고 최적화된 런타임이다. 사실, ASP.NET 5 프로젝트를 새로 만들면 닷넷 프레임워크 뿐만 아니라 닷넷 코어도 기본적으로 사용하도록 설정되어 있다. 

아래는 이 글에서 다룰 내용이다.

In this article:
	- `What is .NET Core`_?
	- `Motivation Behind .NET Core`_
	- `Building Applications with .NET Core`_
	- `.NET Core and NuGet`_
	- `Additional Reading`_

 
What is .NET Core
^^^^^^^^^^^^^^^^^

.NET Core 5 is a modular runtime and library implementation that includes a subset of the .NET Framework. Currently it is feature complete on Windows, and in-progress builds exist for both Linux and OS X. .NET Core consists of a set of libraries, called "CoreFX", and a small, optimized runtime, called "CoreCLR". .NET Core is open-source, so you can follow progress on the project and contribute to it on GitHub:

닷넷 코어 5는 모듈화된 런타임이면서 닷넷 프레임워크를 잘게 쪼개 구현한 라이브러리다. 현재 버전은 윈도우에서는 기능구현이 완료되었지만 리눅스와 OS X 를 위한 빌드가 계속 진행되고 있다. 닷넷 코어는 "CoreFX"라고 부르는 잘게 쪼개진 라이브러리들의 집합과 "CoreCLR" 이라고 부르는 작고 최적화된 런타임으로 구성된다. 또한, 오픈소스 프로젝트이므로 그 진행 과정을 팔로우할 수 있고 깃헙에 컨트리뷰트할 수도 있다. 

	- `.NET Core Libraries (CoreFX) <https://github.com/dotnet/corefx>`_
	- `.NET Core Common Language Runtime (CoreCLR) <https://github.com/dotnet/coreCLR>`_

The CoreCLR runtime (Microsoft.CoreCLR) and CoreFX libraries are distributed via NuGet. The CoreFX libraries are factored as individual NuGet packages according to functionality, named "System.[module]" on `nuget.org <http://www.nuget.org/>`_.

CoreCLR 런타임(Microsoft.CoreCLR)과 CoreFX 라이브러리들은 NuGet을 통해 배포된다. CoreFX 라이브러리들은 그 기능에 따라 "System.[module]" 이라는 이름으로 개별 NuGet 패키지화 되어있다. 

One of the key benefits of .NET Core is its portability. You can package and deploy the CoreCLR with your application, eliminating your application's dependency on an installed version of .NET (e.g. .NET Framework on Windows). You can host multiple applications side-by-side using different versions of the CoreCLR, and upgrade them individually, rather than being forced to upgrade all of them simultaneously.

닷넷 코어의 최고 잇점은 이식(가능)성이다. 애플리케이션과 함께 CoreCLR을 패키지해서 배포할 수 있다는 것은 배포할 서버에 설치되어 있는 닷넷 프레임워크의 버전에 대해 전혀 걱정하지 않아도 된다는 것을 의미한다 (역주: 참고로 Windows 2003에 닷넷 프레임워크를 설치할 수 없다. 이를 배포 시점에 깨닫고 프로젝트의 아키텍쳐를 바꿔야 했던 재밌는 경험이 있다). 따라서, 여러 애플리케이션을 다른 버전의 CoreCLR으로 side-by-side 호스팅할 수 있고 각 애플리케이션을 개별적으로 업그레이드할 수 있다. 런타임 변경에 의해 모든 애플리케이션을 한 번에 업그레이드하도록 강요받지 않는다.   

CoreFX has been built as a componentized set of libraries, each requiring the minimum set of library dependencies (e.g. System.Collections only depends on System.Runtime, not System.Xml). This approach enables minimal distributions  of CoreFX libraries (just the ones you need) within an application, alongside CoreCLR. CoreFX includes collections, console access, diagnostics, IO, LINQ, JSON, XML, and regular expression support, just to name a few libraries. Another benefit of CoreFX is that it allows developers to target a single common set of libraries that are supported by multiple platforms. 

CoreFX는 컴포넌트화된 라이브러리로 각각은 최소한의 라이브러리에 대해서만 종속성을 갖게 설계되었다. 예를 들어, System.Collections 는 Systems.Runtime만 필요하고 Sysmte.Xml에는 의존하지 않는다. 이런 접근법은 애플리케이션과 CoreCLR을 따라 필요한 CoreFX 라이브러리들만 추가함으로써 배포를 최소화할 수 있게 만들어준다. CoreFX는 collections, console access, diagnostics, IO, LINQ, JSON, XML, regular expression 등 적은 수의 라이브러리들을 제공한다. CoreFX의 다른 잇점은 개발자들이 멀티 플랫폼에서 지원되는 단일한 공통의 라이브러리들을 대상으로 작업할 수 있게 해준다는 것이다(역주: 멀티 플랫폼에서 지원되는 단일한 공통의 라이브러리라는 것이 어떤 의미를 갖는지 역자의 블로그 포스트 `닷넷 코어 <http://blog.jakeymvc.com/net-core/>`_ 를 읽어 보자. 마이크로소프트에서 개발 프레임워크를 확실하게 정리하고 있다는 것을 알 수 있을 것이다).

Motivation Behind .NET Core
^^^^^^^^^^^^^^^^^^^^^^^^^^^

When .NET first shipped in 2002, it was a single framework, but it didn't take long before the .NET Compact Framework shipped, providing a smaller version of .NET designed for mobile devices. Over the years, this exercise was repeated multiple times, so that today there are different flavors of .NET specific to different platforms. Add to this the further platform reach provided by Mono and Xamarin, which target Linux, Mac, and native iOS and Android devices. For each platform, a separate vertical stack consisting of runtime, framework, and app model is required to develop .NET applications. One of the primary goals of .NET Core is to provide a single, modular, cross-platform version of .NET that works the same across all of these platforms. Since .NET Core is a fully open source project, the Mono community can benefit from CoreFX libraries. .NET Core will not replace Mono, but it will allow the Mono community to reference and share, rather than duplicate, certain common libraries, and to contribute directly to CoreFX, if desired.

닷넷이 2002년에 처음 도입되었을 때 그 것은 단일 프레임워크였다. 그러나, 얼마 지나지 않아 닷넷 컴팩트 프레임워크가 도입되었고 그 이유는 모바일 기기를 지원하기 위한 경량 버전의 닷넷이 필요했기 때문이다. 해가 지나면서 이런 패턴이 반복되어 오늘 날에는 플랫폼 특화된 여러 종류의 닷넷이 공존하고 있다. 이와 더불어 미래의 플랫폼은, 리눅스와 맥을 대상으로 하는 Mono, Xamarin 그리고 네이티브 iOS와 안드로이드를 지원하도록 그 영역을 넓히고 있다. 각각의 플랫폼에서는 닷넷 애플리케이션을 개발하기 위해 플랫폼에 고유한 버티컬 스택(런타임, 프레임워크, 앱 모델을 포함)이 사용된다. 닷넷 코어의 주된 목표중 한 가지는 단일의, 모듈화된, 크로스플랫폼 버전의 닷넷을 제공함으로써 여러분의 애플리케이션이 여러 다른 플랫폼에서 똑 같이 동작하게 하는 것이다. 닷넷 코어는 완전한 오픈소스 프로젝트이기 때문에 Mono 커뮤니티는 CoreFX 라이브러리들을 사용할 수 있는 잇점이 있다. 닷넷 코어는 Mono 를 대신하지 않을 것이다. Mono 커뮤니티가 공통의 라이브러리들을 중복해서 만드는 대신 CoreFX 라이브러리들을 참조, 공유하기를 바라며 (희망한다면) CoreFX에 직접 기여할 수도 있겠다.

In addition to being able to target a variety of different device platforms, there was also pressure from the server side to reduce the overall footprint, and more importantly, surface area, of the .NET Framework. By factoring the CoreFX libraries and allowing individual applications to pull in only those parts of CoreFX they require (a so-called "pay-for-play" model), server-based applications built with ASP.NET 5 can minimize their dependencies. This, in turn, reduces the frequency with which patches and updates to the framework will impact these applications, since only changes made to the individual pieces of CoreFX leveraged by the application will impact the application. A smaller deployment size for the application is a side benefit, and one that makes more of a difference if many applications are deployed side-by-side on a given server.

여러 다른 기기의 플랫폼을 타켓팅할 수 있는 것과 더불어 서버단으로부터는 전체적인 크기(닷넷 프레임워크의 표면적)를 줄여야 한다 는 압력이 있었다. CoreFX 라이브러리로 개별 요소화함으로써 애플리케이션은 필요한 CoreFX 만 끌어다 쓸 수 있게 되었다. 그 덕에 ASP.NET 5 기반의 서버 애플리케이션은 종속성을 최소화할 수 있는데 이런 방식을 종량제(pay-for-play) 모델이라고 한다. 잘게 쪼개져 나누어진 CoreFX 라이브러리는 업데이트나 패치 주기를 짧게 가져갈 수 있게 되었다. 따라서, 애플리케이션이 의존하는 CoreFX 라이브러리들에 적용된 업데이트만 애플리케이션에 영향을 주기 때문에 업데이트의 부작용도 최소화할 수 있게 되었다. 작은 배포 단위는 애플이케이션이 닷넷 코어를 통해 얻을 수 있는 부가적인 혜택인데, 만약 많은 애플리케이션이 한 서버에서 병렬(side-by-side)로 운영되고 있다면 그 혜택은 더욱 클 것이다.

.. note:: The overall size of .NET Core doesn't intend to be smaller than the .NET Framework over time, but since it is pay-for-play, most applications that utilize only parts of CoreFX will have a smaller deployment footprint.


.. note:: (역주: 닷넷 코어는 컴포넌트화된 CoreFX 라이브러리들과 CoreCLR로 구성되었다는 것을 상기하면서) 닷넷 코어의 전체 크기를 합한 것이 닷넷 프레임워크의 크기보다 작아야 한다고 의도하지는 않는다. 그러나, 종량제 모델의 혜택으로 대부분의 애플리케이션들은 필요한 CoreFX만 골라 쓰는 것으로 애플리케이션의 배포 크기를 훨씬 줄일 수 있다.  

Building Applications with .NET Core
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.NET Core can be used to build a variety of applications using different application models including Web applications, console applications and native mobile applications. The .NET Execution Environment (DNX) provides a cross-platform runtime host that you can use to build .NET Core based applications that can run on Windows, Mac and Linux and is the foundation for running ASP.NET applications on .NET Core. Applications running on DNX can target the .NET Framework or .NET Core. In fact, DNX projects can be cross-compiled, targeting both of these frameworks in a single project, and this is how the project templates ship with Visual Studio 2015. For example, the ``frameworks`` section of *project.json* in a new ASP.NET 5 web project will target *dnx451* and *dnxcore50* by default:

닷넷 코어는 웹 , 콘솔, 네이티브 모바일 애플리케이션을 포함하는 다른 종류의 애플리케이션 모델을 사용하여 다양한 애플리케이션을 작성하는데 사용될 수 있다. 닷넷 실행 환경(DNX - .NET Execution Environment)은 윈도우, 맥, 리눅스에서 동작하는 닷넷 코어 기반의 애플리케이션을 위한 크로스플랫폼 런타임 호스트를 제공한다. DNX는 또한, 닷넷 코어 위에서 ASP.NET 애플리케이션을 실행하기 위한 기반이다. DNX 기반 위에 동작하는 애플리케이션들은 닷넷 프레임워크 또는 닷넷 코어를 타겟으로 할 수 있다. 사실, DNX 프로젝트는 단일 프로젝트에서 두 개의 프레임워크를 타겟으로 하는 크로스 컴파일도 가능하다. 크로스 컴파일은 비주얼스튜디오 2015가 제공하는 프로젝트 템플릿의 기본 구성이기도 하다. 예를 들어, 새 ASP.NET 웹 프로젝트에서 *project.json* 파일의 ``frameworks`` 섹션은 기본적으로 *dnx451* 과 *dnxcore50*를 타켓으로 한다. 


.. code-block:: javascript

	"frameworks": {
		"dnx451": { },
		"dnxcore50": { }
	},

``dnx451`` represents the .NET Framework, while ``dnxcore50`` represents .NET Core 5 (5.0). You can use compiler directives (``#if``) to check for symbols that correspond to the two frameworks: ``DNX451`` and ``DNXCORE50``. If for instance you have code that uses resources that are not available as part of .NET Core, you can surround them in a conditional compilation directive:

``dnx451`` 은 닷넷 프레임워크를 표현하는 반면, ``dnxcore50``은 닷넷 코어 5 (5.0)을 의미한다. 컴파일러 지시자 (``#if``)를 사용해서 두 개의 프레임워크에 각각 해당하는 심볼(``DNX451``과 ``DNXCORE50``)을 확인하는 것으로 프레임워크에 국한된 코딩을 할 수도 있다. 예를 들어, 닷넷 코어에 없는 리소스를 사용하는 코드가 있다면 조건 컴파일 지시어로 해당 코드를 감싸면 된다.

.. code-block:: c#

	#if DNX451
		// utilize resource only available with .NET Framework
	#endif

The recommendation from the ASP.NET team is to target both frameworks with new applications. If you want to only target .NET Core, remove *dnx451*, or only target .NET Framework, remove *dnxcore50*, from the *frameworks* listed in *project.json*. Note that ASP.NET 4.6 and earlier target and require the .NET Framework, as they always have.

ASP.NET 팀은 새 애플리케이션에서 두 개의 프레임워크를 타겟으로 할 것을 추천한다. 닷넷 코어만 타겟으로 한다면 *dnx451*을 삭제하고, 닷넷 프레임워크만을 위해서는 *dnxcore50*을 *framework* 목록에서 제거한다. ASP.NET 4.6과 그 이전 버전은 항상 닷넷 프레임워크를 타겟으로 해야한다는 것에 유의하자.

.NET Core and NuGet
^^^^^^^^^^^^^^^^^^^

Using NuGet allows for much more agile usage of the individual libraries that comprise .NET Core. It also means that an application can list a collection of NuGet packages (and associated version information) and this will comprise both system/framework as well as third-party dependencies required. Further, third-party dependencies can now also express their specific dependencies on framework features, making it much easier to ensure the proper packages and versions are pulled together during the development and build process.

NuGet을 사용하는 방식은 닷넷 코어를 구성하는 개별 라이브러리들을 훨씬 빠르고 쉽게 사용하도록 해준다. 이 것이 의미하는건, 애플리케이션이 버전 정보를 포함한 NuGet 패키지들을 지정함으로써 시스템, 프레임워크 뿐만 아니라 써드파티 종속성까지 구성한다는 것이다. 더 나아가면, 써드파티 종속성은 이제 프레임워크 특징에 의존적인 특정 종속성도 표현할 수도 있게 되어 알맞은 패키지들과 버전들이 개발과 빌드 과정에서 확실히 조합될 수 있도록 하는 것이 훨씬 쉬워졌다.     

If, for example, you need to use immutable collections, you can install the System.Collections.Immutable package via NuGet. The NuGet version will also align with the assembly version, and will use `semantic versioning <http://semver.org>`_.

예를 들어 만약, 수정할 수 없는 컬렉션을 사용해야 한다면 NuGet을 통해 System.Collections.Immutable 패키지를 설치할 수 있다. NuGet 버전은 어셈블리 버전을 나란히 결정할 것이고 `의미 있는 버저닝 (semantic versioning)  <http://semver.org>`_ 을 할 것이다.

.. note:: Although CoreFX will be made available as a fairly large number of individual NuGet packages, it will continue to ship periodically as a full unit that Microsoft has tested as a whole. These distributions will most likely ship at a lower cadence than individual packages, allowing time to perform necessary testing, fixes, and the distribution process.

..note:: CoreFX는 꽤 많은 양이 NuGet 패키지로 사용 가능하게 되겠지만 마이크로소프트가 전체를 하나로 테스트한 하나의 큰 덩어리로도 주기적으로 배포될 것이다. 이런 배포들은 충분히 시간을 두고 테스트, 수정, 배포 과정을 거치기 때문에 개별 패키지보다는 느린 보조로 제공될 것이다. 

Summary
^^^^^^^

.NET Core is a modular, streamlined subset of the .NET Framework and CLR. It is fully open-source and provides a common set of libraries that can be targeted across numerous platforms. Its factored approach allows applications to take dependencies only on those portions of the CoreFX that they use, and the smaller runtime is ideal for deployment to both small devices (though it doesn't yet support any) as well as cloud-optimized environments that need to be able to run many small applications side-by-side. Support for targeting .NET Core is built into the ASP.NET 5 project templates that ship with Visual Studio 2015.

닷넷 코어는 닷넷 프레임워크의 모듈화되고 간소화된 서브셋이고 CLR이다. 닷넷 코어는 완전한 오픈소스이고 여러 플랫폼을 타겟으로 하는 공통의 라이브러리 모음을 제공한다. 닷넷 코어의 잘게 요소화된 접근법은 애플리케이션들이 CoreFX의 필요한 부분에만 최소한의 종속성을 갖게 해주고 경량화된 런타임은 작은 기기뿐 아니라 수 많은 작은 애플리케이션들을 병렬로 동시에 운영해야 하는 클라우드 최적화된 환경에도 적합하다. 닷넷 코어를 타켓으로 하는 것은 비주얼스튜디오 2015의 ASP.NET 5 프로젝트 템플릿에 포함되어 있다.

Additional Reading
^^^^^^^^^^^^^^^^^^

Learn more about .NET Core:
	- `Immo Landwerth Explains .NET Core <http://blogs.msdn.com/b/dotnet/archive/2014/12/04/introducing-net-core.aspx>`_
	- `What is .NET Core 5 and ASP.NET 5 <http://blogs.msdn.com/b/cesardelatorre/archive/2014/11/18/what-is-net-core-5-and-asp-net-5-within-net-2015-preview.aspx>`_
	- `.NET Core 5 on dotnetfoundation.org <https://www.dotnetfoundation.org/netcore>`_
	- `.NET Core is Open Source <http://blogs.msdn.com/b/dotnet/archive/2014/11/12/net-core-is-open-source.aspx>`_
	- `.NET Core on GitHub <https://github.com/dotnet/corefx>`_

