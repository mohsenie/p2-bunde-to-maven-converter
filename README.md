# p2 bundle to maven module converter
this project converts SWT bundle from eclipse P2 repository to a Maven module.
You need to compile the P2 bundle into a standard Maven module then use it as a dependency in your project.

there is a sample project included under SwtSample which uses the generated Jar file as a dependency.

to compile any P2 dependency into a Maven module open the MANIFEST.MF and change Require-Bundle to whatever eclipse bundle you need
then just run: 

`mvn clean package`

the output is a file called "swt-3.115.0-SNAPSHOT-repackaged.jar" which you can use to install as a local mavan M2 dependency.
to use the repackaged jar file as dependency inside sample project just cd into P2BundleConverter and use below command

`mvn clean compile package initialize`

this project uses Tycho maven plugin > https://wiki.eclipse.org/Tycho/Migration_Howto

Note: since the build is platform specific you need to define what platform you are repackaging the P2 bundle for. that is defined using "target-platform-configuration" plugin of Tycho. for example to package for linux use

<environment>
    <os>linux</os>
    <ws>gtk</ws>
    <arch>x86_64</arch>
</environment>

or for windows :

<environment>
	<os>win32</os>
    <ws>win32</ws>
    <arch>x86_64</arch>
</environment>