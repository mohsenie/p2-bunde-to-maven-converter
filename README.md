# p2 bundle to maven module converter
this project converts SWT bundle from eclipse P2 repository to a Maven module.
You need to compile the P2 bundle into a standard Maven module then use it as a dependency in your project.

to compile any P2 dependency into a Maven module open the MANIFEST.MF and change Require-Bundle to whatever eclipse bundle you need
then just run below command:

`mvn package`

In case you are repackaging other P2 bundles obviously other specifics such as groupId and artifactId in the pom file need to be change accordignly.

in the case of this bundle the output is a file called "swt-3.115.0-SNAPSHOT-repackaged.jar" which is automatically installed to local mavan M2 repository. The sample project included under SwtSample uses the generated Jar file as a dependency which again is automatically installed to your local m2 repositoy so you should be able to run the sample project as is.

this project uses Tycho maven plugin > https://wiki.eclipse.org/Tycho

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
