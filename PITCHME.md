---?image=assets/images/gitpitch-audience.jpg
@title[EDK_II_Porting_Projects_pres]
<br><br><br>
<span style="font-size:0.75em" >This slide deck has moved to:  https://gitpitch.com/tianocore-training/EDK_II_Porting_Projects_pres/master#/
</span>
<br><br>
## <span class="gold"   >UEFI & EDK II Training</span>

#### Porting an Existing Project 

<br>
<span style="font-size:0.75em" ><a href='http://www.tianocore.org'>tianocore.org</a></span>
Note:
  PITCHME.md for UEFI / EDK II Training  Porting an Existing Project with EDK II

  Copyright (c) 2018, Intel Corporation. All rights reserved.<BR>

  Redistribution and use in source (original document form) and 'compiled'
  forms (converted to PDF, epub, HTML and other formats) with or without
  modification, are permitted provided that the following conditions are met:

  1) Redistributions of source code (original document form) must retain the
     above copyright notice, this list of conditions and the following
     disclaimer as the first lines of this file unmodified.

  2) Redistributions in compiled form (transformed to other DTDs, converted to
     PDF, epub, HTML and other formats) must reproduce the above copyright
     notice, this list of conditions and the following disclaimer in the
     documentation and/or other materials provided with the distribution.

  THIS DOCUMENTATION IS PROVIDED BY TIANOCORE PROJECT "AS IS" AND ANY EXPRESS OR
  IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF
  MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO
  EVENT SHALL TIANOCORE PROJECT  BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL,
  SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO,
  PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS;
  OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY,
  WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR
  OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS DOCUMENTATION, EVEN IF
  ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.



---  
@title[Lesson Objective]
<BR>
### <p align="center"<span class="gold"   >Lesson Objective </span></p><br>

<!---  Add bullets using https://fontawesome.com/cheatsheet certificate
-->
<ul style="list-style-type:none">
 <li>@fa[certificate gp-bullet-green]<span style="font-size:0.9em">&nbsp;&nbsp;Define the porting task list for porting existing<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; platforms in EDK II in order to boot to the UEFI Shell</span> </li>
 <li>@fa[certificate gp-bullet-cyan]<span style="font-size:0.9em">&nbsp;&nbsp;Explain the EDK II infrastructure, porting libraries,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; library classes, PCDs, and directory structures</span></li>
 <li>@fa[certificate gp-bullet-yellow]<span style="font-size:0.9em">&nbsp;&nbsp;Determine the necessary porting for each phase<br> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;of a new EDK II platform Project</span> </li>
</ul>

---?image=assets/images/binary-strings-black2.jpg
@title[EDK II Infrastructure Section]
<br><br><br><br><br><br><br>
### <span class="gold"  >&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;EDK II Infrastructure </span>
<span style="font-size:0.9em" >&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Review of EDK II</span>


---
@title[EDK II Infrastructure]
<p align="right"><span class="gold" ><b>EDK II Infrastructure</b></span></p>

@snap[north-west span-60 fragment]
<br>
<br>
<br>
@box[bg-gold2 text-white rounded my-box-pad2  ](<p style="line-height:70%" ><span style="font-size:0.9em; font-weight: bold;" >Directory Structure<br>&nbsp;</span></p>)
<br>
@snapend


@snap[north-east span-65 fragment]
<br>
<br>
<br>
<p style="line-height:50%" ><br><br><br>&nbsp;</p>
@box[bg-royal text-white rounded my-box-pad2  ](<p style="line-height:70%" ><span style="font-size:0.9em; font-weight: bold;" >Platform/Projects in Packages<br>&nbsp;</span></p>)
<br>
@snapend


@snap[north-west span-70 fragment]
<br>
<br>
<br>
<br>
<br>
<br>
<p style="line-height:50%" ><br><br><br>&nbsp;</p>
@box[bg-purple-pp text-white rounded my-box-pad2  ](<p style="line-height:70%" ><span style="font-size:0.9em; font-weight: bold;" > Library Class Name &rarr; Instance <br>&nbsp;</span></p>)
<br>
@snapend



@snap[north-east span-80 fragment]
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<p style="line-height:50%" ><br><br><br><br>&nbsp;<br>&nbsp;</p>
@box[bg-navy text-white rounded my-box-pad2  ](<p style="line-height:70%" ><span style="font-size:0.9em; font-weight: bold;" >Platform Configuration Database PCD<br>&nbsp;</span></p>)
<br>
@snapend






Note:

- First off we have the infrastructure.
- So the infrastructure is what are the new things added for EDK II?

- First, the directory structure, the directory structure for EDK II is now structured so that all of the platform package contents are in subdirectories under the platform package. So we will have a new platform package, and in that directory there will be subdirectories where we will have all of the reported modules and code for our new platform. Anything we update will be in this directory package. So what we will see is our build description files.

- The other thing that is different is the libraries. We see with EDK II we have a library class and library instances. If we take our existing platform and look at the library instances we may have to update those for our new platform package.

- The third thing that is different is the new platform configuration database or PCD. What we will see with this is to port our new platform we may only be changing a PCD value and we may not even change the source code.

- Directory Structure
  - The package for the platform contains subdirectories for ported modules
  - Text files: FDF, DSC, DEC

- Libraries – Library class and library instances may need to be ported for the platform

- PCD – PCD helps with porting, and may mean not changing any of the source code


---
@title[EDK II Infrastructure Review]
<p align="right"><span class="gold" ><b>EDK II Infrastructure - review</b></span></p>


@snap[west span-30 ]
@box[bg-royal text-white waved fragment](<span style="font-size:01.25em" >@color[yellow](<b>Packages</b>)</span><br>List of related modules )
@snapend


@snap[north-west span-45 fragment]
@css[text-yellow]( <br><br><br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="font-size:03.25em" >+</span>)
@snapend


@snap[midpoint span-30 ]
@box[bg-royal text-white waved fragment](<span style="font-size:01.25em" >@color[yellow](<b>Libraries</b>)</span> Same name & interface)
@snapend

@snap[north span-45 fragment]
@css[text-yellow]( <br><br><br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="font-size:03.25em" >+</span>)
@snapend

@snap[east span-30]
@box[bg-royal text-white waved fragment](<span style="font-size:01.25em" >@color[yellow](<b>PCDs</b>) </span><br> Platform Config. DB )
@snapend


Note:

Infrastructure Summary <br>
- Packages<br>
  - list of modules<br>
- Libraries<br>
   - Same Names with different implementation but same interface<br>
- PCD
  - Platform configuration database



---
@title[New Package Directory]
<p align="right"><span class="gold" ><b>New Package Directory</b></span></p>

@snap[north-west span-50 ]
<br>
<br>
@box[bg-black text-white rounded my-box-pad2  ](<p style="line-height:70%" ><span style="font-size:0.9em; font-weight: bold;" > <br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>&nbsp;</span></p>)
<br>
@snapend

@snap[north-west span-50 ]
<br>
<br>
<p style="line-height:85%" align="left"><span style="font-size:0.65em; font-family:Consolas;" > 
&nbsp;&nbsp; MyWorkSpace/ <br>
&nbsp;&nbsp;&nbsp;&nbsp; . . . <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; NewProjectPkg/ <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Include/ <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Library/ <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; . . . <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; PlatformDrivers/ <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br>
</span></p>
@snapend

@snap[north-west span-50 fragment]
<br>
<br>
<p style="line-height:85%" align="left"><span style="font-size:0.65em; font-family:Consolas;" > 
&nbsp;&nbsp; MyWorkSpace/ <br>
&nbsp;&nbsp;&nbsp;&nbsp; . . . <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; NewProjectPkg/ <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Include/ <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Library/ <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; . . . <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; PlatformDrivers/ <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#00b0f0">NewProjectPkg.DSC</font><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br>
</span></p>
@snapend

@snap[north-east span-45 fragment ]
<br>
<br>
@box[bg-yellow text-black my-box-pad2  ](<p style="line-height:75%" align="left"><span style="font-size:0.85em">&nbsp;&nbsp;<font color="blue"><b>DSC</b></font></span><span style="font-size:0.75em"><br>&nbsp;&nbsp;Only one to build against <br>&nbsp;&nbsp;Contains PCD platform values <br>&nbsp;&nbsp;Defines library classes<br>&nbsp;&nbsp;Includes other modules<br>&nbsp;&nbsp;</span></p>)
@snapend

@snap[north-west span-50 fragment]
<br>
<br>
<p style="line-height:85%" align="left"><span style="font-size:0.65em; font-family:Consolas;" > 
&nbsp;&nbsp; MyWorkSpace/ <br>
&nbsp;&nbsp;&nbsp;&nbsp; . . . <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; NewProjectPkg/ <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Include/ <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Library/ <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; . . . <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; PlatformDrivers/ <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#00b0f0">NewProjectPkg.DSC</font><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="red">NewProjectPkg.FDF</font><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<br>
</span></p>
@snapend


@snap[north-east span-45 fragment ]
<br>
<br>
<br>
<br>
<br>
<p style="line-height:75%" align="left"> <br><br>&nbsp;&nbsp;</p>
@box[bg-yellow text-black my-box-pad2  ](<p style="line-height:75%" align="left"><span style="font-size:0.85em">&nbsp;&nbsp;<font color="red"><b>FDF</b></font></span><span style="font-size:0.75em"><br>&nbsp;&nbsp;File to define flash layout<br>&nbsp;&nbsp;</span></p>)
@snapend

@snap[north-west span-50 fragment]
<br>
<br>
<p style="line-height:85%" align="left"><span style="font-size:0.65em; font-family:Consolas;" > 
&nbsp;&nbsp; MyWorkSpace/ <br>
&nbsp;&nbsp;&nbsp;&nbsp; . . . <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; NewProjectPkg/ <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Include/ <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Library/ <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; . . . <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; PlatformDrivers/ <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#00b0f0">NewProjectPkg.DSC</font><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="red">NewProjectPkg.FDF</font><br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#87E2A9">NewProjectPkg.DEC</font><br>
</span></p>
@snapend

@snap[north-east span-45 fragment ]
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
@box[bg-yellow text-black my-box-pad2  ](<p style="line-height:75%" align="left"><span style="font-size:0.85em">&nbsp;&nbsp;<font color="green"><b>DEC</b></font></span><span style="font-size:0.75em"><br>&nbsp;&nbsp;File to define PCDS within the<br>&nbsp;&nbsp; Platform Package <br>&nbsp;&nbsp;</span></p>)
@snapend


Note:

---?image=/assets/images/slides/Slide7_1.JPG
@title[Libraries]
<br>
<p align="center"><span style="font-size:01.25em"><font color="#e49436"><b>Libraries</b></font></span></p>



@snap[north-east span-80 fragment ]
<br>
<br>
<br>
<br>
<p style="line-height:75%" align="left"><span style="font-size:0.9em">@color[yellow](DSC maps library class to library-instances)</span></p>
<br>
@snapend


@snap[north-east span-80 fragment ]
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<p style="line-height:75%" align="left"><span style="font-size:0.9em">Syntax in DSC File</span><br>
<span style="font-size:0.65em; font-family:Consolas;">
&nbsp;&nbsp;&nbsp;&nbsp;[libraryclasses] <br>
&nbsp;&nbsp;&nbsp;&nbsp;LibraryClassName|Path/To/@color[#00ffff](LibInstanceNameInstance1).inf  </span> </p>  
<br>
@snapend


@snap[south span-85 fragment ]
@box[bg-purple-pp text-white rounded   ](<span style="font-size:01.0em" >Search INF files for string:&nbsp;&nbsp; "`LIBRARY_CLASS  =`"&nbsp;</span>)
<br>
@snapend

Note:

- DSC maps library-class to library-instances
- Global, by type, individual override based on desired implimentation
- Effected by size, speed, built in, binary distribution 
- PCI example
  - PciCfg – Protocol function call by GUID (PEI)
  - PciRootBridgeIo – Protocol function call by GUID (DXE)
  - Syntax in DSC file
  - 	[libraryclasses] 
  - 	LibraryClassName|Path/To/LibInstanceNameInstance1.inf
  
  
- another Note; Workspace relative paths!
  -  Check for existing library instances.
  - Search workspace INF files for string: "LIBRARY_CLASS  ="



---
@title[Library Classes in DSC ]
<p align="right"><span class="gold" ><b>Library Classes Section in DSC<b></span></p>

<p style="line-height:70%" ><span style="font-size:0.9em; font-weight: bold;" >`DebugLib` class in `NewProjectPkg.dsc` </span></p>
<br>
```
 [LibraryClasses]
     DebugLib|MdePkg/Library/BaseDebugLibNull/BaseDebugLibNull.inf
     • • •
 [LibraryClasses.common.DXE_CORE]
         • • •
    DebugLib|IntelFrameworkModulePkg/Library/PeiDxeDebugLibReportStatusCode/
           PeiDxeDebugLibReportStatusCode.inf  
        • • •
 [LibraryClasses.common.DXE_SMM_DRIVER]
    DebugLib|MdePkg/Library/BaseDebugLibNull/BaseDebugLibNull.inf

```
<hr>
```
 [Components]
      • • •
 MyPath/MyModule.inf {
  <LibraryClasses>
    DebugLib|MdePkg/Library/BaseDebugLibSerialPort.inf
 }
 
``` 
@snap[north-east span-30 fragment ]
<br>
<br>
<br>
<br>
@box[bg-purple-pp text-white my-box-pad2  ](<span style="font-size:0.6em;"> Library Class Section</span>)
<br>
<br>
<br>
<br>
<br>
@box[bg-green text-white my-box-pad2  ](<span style="font-size:0.6em;"> Components Section</span>)
@snapend



Note:

Example - 

<pre>
 DebugLib class in NewProjectPkg.dsc

 [LibraryClasses]
     DebugLib|MdePkg/Library/BaseDebugLibNull/BaseDebugLibNull.inf
     • • •
 [LibraryClasses.common.DXE_CORE]
         • • •
    DebugLib|IntelFrameworkModulePkg/Library/PeiDxeDebugLibReportStatusCode/
           PeiDxeDebugLibReportStatusCode.inf  
        • • •
 [LibraryClasses.common.DXE_SMM_DRIVER]
    DebugLib|MdePkg/Library/BaseDebugLibNull/BaseDebugLibNull.inf

 [Components]
      • • •
 MyPath/MyModule.inf {
  <LibraryClasses>
    DebugLib|MdePkg/Library/BaseDebugLibSerialPort.inf
 }
</pre>




---
@title[PCD Types]
<p align="right"><span class="gold" ><b>PCD Types</b></span></p>
@snap[east span-35]
@box[bg-lt-blue-pp text-white rounded my-box-pad2  ](<p style="line-height:80%" ><span style="font-size:0.80em; font-family: Courier New; font-weight: bold;" > FeatureFlag</span></p>)
<br>
@snapend

@snap[north-west span-35]
<br>
<br>
@box[bg-yellow text-blue rounded my-box-pad2  ](<p style="line-height:80%" ><span style="font-size:0.80em; font-family: Courier New; font-weight: bold;" > FixedAtBuild</span></p>)
@snapend


@snap[north span-30]
<br>
<br>
<br>
<br>
@box[bg-green-pp text-white rounded my-box-pad2  ](<p style="line-height:80%" ><span style="font-size:0.80em; font-family: Courier New; font-weight: bold;" > Dynamic</span></p>)
@snapend


@snap[north-east span-30]
<br>
<br>
@box[bg-green-pp text-white rounded my-box-pad2  ](<p style="line-height:80%" ><span style="font-size:0.80em; font-family: Courier New; font-weight: bold;" > DynamicEx</span></p>)
@snapend



@snap[south-west span-30]
@box[bg-green-pp text-white rounded my-box-pad2  ](<p style="line-height:80%" ><span style="font-size:0.80em; font-family: Courier New; font-weight: bold;" > DynamicHii</span></p>)
<br>
<br>
<br>
<br>
<br>
@snapend

@snap[south-east span-30]
@box[bg-green-pp text-white rounded my-box-pad2  ](<p style="line-height:80%" ><span style="font-size:0.80em; font-family: Courier New; font-weight: bold;" > DynamicVpd</span></p>)
<br>
<br>
<br>
<br>
<br>
@snapend


@snap[west span-45]
@box[bg-purple-pp text-white rounded my-box-pad2  ](<p style="line-height:80%" ><span style="font-size:0.80em; font-family: Courier New; font-weight: bold;" > PatchableInModule</span></p>)
<br>
@snapend


@snap[south-west span-100]
@box[bg-navy text-white rounded  my-box-pad2 fragment ](<p style="line-height:80%" ><span style="font-size:0.80em; font-weight: bold;" > Syntax Examples<br></span><span style="font-size:0.50em;" >`[pcdsFeatureFlag.common] [pcdsFixedAtBuild.IA32]`&nbsp;<br>`[PcdsFixedAtBuild, PcdsPatchableInModule, PcdsDynamic, PcdsDynamicEx]`<br>&nbsp;</span></p>)
@snapend

Note:

- FeatureFlag 
  - Replaces a switch MACRO to enable/disable a feature (TRUE or FALSE)
- FixedAtBuild
  - Replaces a macro that produced a customizable value
  - Value of this PCD type is determined at build time and is stored in the code section of a module’s PE image 
- PatchableInModule
  - Value is stored in the data section, rather than the code section, of the module’s PE image. 
- Dynamic / DyanmicEx / DynamicHii / DynamicVpd
  - Value is assigned by one module and is accessed by other modules in execution time 
- Syntax Examples
	- [pcdsFeatureFlag.common] [pcdsFixedAtBuild.IA32] [pcdsFixedAtBuild.X64]   [pcdsFixedAtBuild.IPF] [pcdsFixedAtBuild.EBC]   [pcdsDynamic.IA32] [pcdsDynamicEx.X64] 



---?image=/assets/images/slides/Slide10_1.JPG
@title[PCD Syntax]
<p align="right"><span class="gold" ><b>PCD Syntax</b></span></p>
@snap[north-east span-90 fragment]
<br>
<br>
<p align="left" style="line-height:80%"><span style="font-size:0.9em; ">PCD defined in the DEC file from any package</span></p>
@box[bg-black text-white my-box-pad2  ](<p style="line-height:40%" align="left"><span style="font-size:0.450em; font-family:Consolas; " >&nbsp;&nbsp;[Guids.common]<br>&nbsp;&nbsp;@color[red](PcdTokenSpaceGuidName)={ 0xXXXXXXXX, 0xXXXX, 0xXXXX, { 0xXX, . . .}}<br>&nbsp;&nbsp;. . .<br>&nbsp;&nbsp;[Pcds...]<br>&nbsp;&nbsp;PcdTokenSpaceGuidName.PcdTokenName|Value[|DatumType[|MaxSize]]|Token<br>&nbsp;&nbsp;</span></p>)
<br>
@snapend

@snap[north-east span-90 fragment]
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<p align="left" style="line-height:80%"><span style="font-size:0.9em; ">PCD usage listed in INF file for module</span></p>
@box[bg-black text-white my-box-pad2  ](<p style="line-height:40%" align="left"><span style="font-size:0.450em; font-family:Consolas; " >&nbsp;&nbsp;[...Pcds...]<br>&nbsp;&nbsp;PcdTokenSpaceGuidName.@color[red](PcdTokenName)|[Value]<br>&nbsp;&nbsp;</span></p>)
<br>
@snapend


@snap[north-east span-90 fragment]
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<p align="left" style="line-height:80%"><span style="font-size:0.9em; ">Value of PCD set in @color[yellow](`NewProject.dsc`)</span></p>
@box[bg-black text-white my-box-pad2  ](<p style="line-height:40%" align="left"><span style="font-size:0.450em; font-family:Consolas; " >&nbsp;&nbsp;[Pcds...]<br>&nbsp;&nbsp;PcdTokenSpaceGuidName.@color[red](PcdTokenName)|Value[|DatumType[|MaximumDatumSize]]</span><br>&nbsp;&nbsp;</p>)
<br>
@snapend


@snap[north-east span-90 fragment]
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
![ExamplePCD](/assets/images/ExamplePCD.png)
@snapend

Note:


- PCD defined in the DEC file from any package
- [Guids.common]
   - PcdTokenSpaceGuidName={ 0x914AEBE7, 0x4635, 0x459b, { 0xAA, . . .}}

- [Pcds...]
  - PcdTokenSpaceGuidName.PcdTokenName|Value[|DatumType[|MaxSize]]|Token
  - PCD usage listed in INF file for module
- […Pcd…] 
  - PcdTokenSpaceGuidName.PcdTokenName|[Value]
  - Value of PCD set in NewPlatform.dsc
- [Pcds...]
  - PcdTokenSpaceGuidName.PcdTokenName|Value[|DatumType[|MaximumDatumSize]]
- Example used in NewProject.dsc
- [PcdsFixedAtBuild.IA32]
  -  gEfiIchTokenSpaceGuid.PcdIchAcpiIoPortBaseAddress|0x400
  -  gNewProjectTokenSpaceGuid.PcdFlashAreaBaseAddress|0xFFF00000
  - gNewProjectTokenSpaceGuid.PcdFlashAreaSize|0x100000
 

---?image=assets/images/binary-strings-black2.jpg
@title[Porting Task List Section]
<br><br><br><br><br><br><br>
### <span class="gold"  >&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Porting Task List</span>
<span style="font-size:0.9em" >&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;What is the best approach for how to port?</span>


---?image=/assets/images/slides/Slide27_1.JPG
@title[Porting Approach]
### <p align="center"><font color="yellow"><b>Approach – Porting EDK II</b></font></p>

@snap[north-east span-45 fragment]
<br>
<br>
<br>
@box[bg-gold2 text-white my-box-pad2  ](<p style="line-height:40%"><span style="font-size:01.1em" > <b>Search Work Space</b><br>&nbsp;</span></p>)
@snapend


@snap[west span-60 fragment]
<br>
<br>
<br>
<br>
@box[bg-royal text-white my-box-pad2  ](<p style="line-height:40%"><span style="font-size:01.1em" ><b>Find Similar EDK II Projects</b><br>&nbsp;</span></p>)
@snapend


@snap[south span-50 fragment]
@box[bg-purple-pp text-white my-box-pad2  ](<p style="line-height:40%"><span style="font-size:01.1em" > <b>Boot to UEFI Shell</b><br>&nbsp;</span></p>)
<br>
@snapend

Note:

- Many examples of packages in the UDK / EDK II source base 
- Find a similar package or platform or project that meets target project needs
-  Build description files are text files using basic text editor to update – no GUI with the goal of booting to the UEFI Shell

Porting_task_list.gif



<!---  Section for Porting Task  -->

---?image=assets/images/binary-strings-black2.jpg
<!-- .slide: data-transition="none" -->
@title[Porting Task List Section]
<p align="center"><span style="font-size:01.25em"><font color="#e49436"><b>Porting Task List</b></span></p>

@snap[north-east span-90 ]
<br>
<br>
<br>
@box[bg-grey-15 text-white rounded my-box-pad2  ](<p style="line-height:60%" ><span style="font-size:0.9em; font-weight: bold;" > <br><br> <br><br><br><br><br><br><br><br><br><br><br><br><br>&nbsp;</span></p>)
@snapend


@snap[north-east span-15]
![Porting_task_list.gif](/assets/images/tenor.gif)
@snapend

<!---  col of numbers  -->

@snap[north-west span-10]
<br>
<br>
<p style="line-height:60%" align="left"><span style="font-size:02.0em" ><font color="#808080"><br>&#10102;<br><br>&#10103;<br><br>&#10104;<br><br>&#10105;<br><br>&#10106;<br><br>&#10107;  </font></span></p>
@snapend
<!---  
1
-->


@snap[north-west span-10 fragment]
<br>
<br>
<p style="line-height:60%" align="left"><span style="font-size:02.0em" ><font color="#808080"><br>@color[yellow](&#10102;)<br><br>&#10103;<br><br>&#10104;<br><br>&#10105;<br><br>&#10106;<br><br>&#10107;  </font></span></p>
@snapend


@snap[north-east span-90 fragment]
<br>
<br>
<p style="line-height:60%" align="left"><span style="font-size:0.85em" ><br>&nbsp;@color[white](Create a New Project package directory)<br><br>&nbsp;<br><br>&nbsp;<br><br>&nbsp;<br><br>&nbsp;<br><br>&nbsp;  </font></span></p>
@snapend
<!---  
2
-->


@snap[north-west span-10 fragment]
<br>
<br>
<p style="line-height:60%" align="left"><span style="font-size:02.0em" ><font color="#808080"><br>@color[yellow](&#10102;<br><br>&#10103;)<br><br>&#10104;<br><br>&#10105;<br><br>&#10106;<br><br>&#10107;  </font></span></p>
@snapend

@snap[north-east span-90 fragment]
<br>
<br>
<p style="line-height:60%" align="left"><span style="font-size:0.85em" ><br>&nbsp;@color[white](Create a New Project package directory)<br><br><br>&nbsp;@color[white](Create Build Files &lpar;DSC, DEC, and FDF&rpar;)<br><br>&nbsp;<br><br>&nbsp;<br><br>&nbsp;  </font></span></p>
@snapend

<!---  
3
-->

@snap[north-west span-10 fragment]
<br>
<br>
<p style="line-height:60%" align="left"><span style="font-size:02.0em" ><font color="#808080"><br>@color[yellow](&#10102;<br><br>&#10103;<br><br>&#10104;)<br><br>&#10105;<br><br>&#10106;<br><br>&#10107;  </font></span></p>
@snapend

@snap[north-east span-90 fragment]
<br>
<br>
<p style="line-height:60%" align="left"><span style="font-size:0.85em" ><br>&nbsp;@color[white](Create a New Project package directory)
<br><br><br>&nbsp;@color[white](Create Build Files &lpar;DSC, DEC, and FDF&rpar;)
<br><br><br>&nbsp;@color[white](Update target.txt to make your Project the default)<br><br>&nbsp;<br><br>&nbsp;  </font></span></p>
@snapend


<!---  
4
-->

@snap[north-west span-10 fragment]
<br>
<br>
<p style="line-height:60%" align="left"><span style="font-size:02.0em" ><font color="#808080"><br>@color[yellow](&#10102;<br><br>&#10103;<br><br>&#10104;<br><br>&#10105;)<br><br>&#10106;<br><br>&#10107;  </font></span></p>
@snapend

@snap[north-east span-90 fragment]
<br>
<br>
<p style="line-height:60%" align="left"><span style="font-size:0.85em" ><br>&nbsp;@color[white](Create a New Project package directory)
<br><br><br>&nbsp;@color[white](Create Build Files &lpar;DSC, DEC, and FDF&rpar;)
<br><br><br>&nbsp;@color[white](Update target.txt to make your Project the default)
<br><br><br>&nbsp;@color[white](Use UEFI PI phases to Port all project modules)
<br><br>&nbsp;  </font></span></p>
@snapend
<!---  
5
-->

@snap[north-west span-10 fragment]
<br>
<br>
<p style="line-height:60%" align="left"><span style="font-size:02.0em" ><font color="#808080"><br>@color[yellow](&#10102;<br><br>&#10103;<br><br>&#10104;<br><br>&#10105;<br><br>&#10106;)<br><br>&#10107;  </font></span></p>
@snapend

@snap[north-east span-90 fragment]
<br>
<br>
<p style="line-height:60%" align="left"><span style="font-size:0.85em" ><br>&nbsp;@color[white](Create a New Project package directory)
<br><br><br>&nbsp;@color[white](Create Build Files &lpar;DSC, DEC, and FDF&rpar;)
<br><br><br>&nbsp;@color[white](Update target.txt to make your Project the default)
<br><br><br>&nbsp;@color[white](Use UEFI PI phases to Port all project modules)
<br><br><br>&nbsp;@color[white](Update DSC w/ new libraries, modules, and PCDs values)
<br><br><br>&nbsp;</font></span></p>
@snapend

<!---  
6 Minimums for UEFI Shell
-->

@snap[north-west span-10 fragment]
<br>
<br>
<p style="line-height:60%" align="left"><span style="font-size:02.0em" ><font color="#808080"><br>@color[yellow](&#10102;<br><br>&#10103;<br><br>&#10104;<br><br>&#10105;<br><br>&#10106;<br><br>&#10107;)  </font></span></p>
@snapend


@snap[north-east span-90 fragment]
<br>
<br>
<p style="line-height:60%" align="left"><span style="font-size:0.85em" ><br>&nbsp;@color[white](Create a New Project package directory)
<br><br><br>&nbsp;@color[white](Create Build Files &lpar;DSC, DEC, and FDF&rpar;)
<br><br><br>&nbsp;@color[white](Update target.txt to make your Project the default)
<br><br><br>&nbsp;@color[white](Use UEFI PI phases to Port all project modules)
<br><br><br>&nbsp;@color[white](Update DSC w/ new libraries, modules, and PCDs values)
<br><br><br>&nbsp;@color[white](Minimums for UEFI Shell)</font></span></p>
@snapend



Note:

1. Create a New Project package directory
2. Create Build Files (DSC, DEC, and FDF)
3. Update conf/target.txt to make your Project the default build (optional)  
4. Port all required modules for your project through all UEFI Platform initialization phases
5. Update build text (DSC, DEC, FDF) files with libraries, ported modules, and PCD values to configure modules
6. Minimums for UEFI Shell


+++?image=assets/images/binary-strings-black2.jpg
<!-- .slide: data-background-transition="none" -->
<!-- .slide: data-transition="none" -->
@title[Porting Task List Section 02]
<p align="center"><span style="font-size:01.25em"><font color="#e49436"><b>Porting Task List</b></span></p>

@snap[north-east span-90 ]
<br>
<br>
<br>
@box[bg-grey-15 text-white rounded my-box-pad2  ](<p style="line-height:60%" ><span style="font-size:0.9em; font-weight: bold;" > <br><br> <br><br><br><br><br><br><br><br><br><br><br><br><br>&nbsp;</span></p>)
@snapend


@snap[north-east span-15]
![Porting_task_list.gif](/assets/images/tenor.gif)
@snapend

<!---  col of numbers  -->


@snap[north-west span-10 ]
<br>
<br>
<p style="line-height:60%" align="left"><span style="font-size:02.0em" ><font color="#808080"><br>@color[yellow](&#10102;<br><br>&#10103;<br><br>&#10104;<br><br>)&#10105;<br><br>&#10106;<br><br>&#10107;  </font></span></p>
@snapend


@snap[north-east span-90 ]
<br>
<br>
<p style="line-height:60%" align="left"><span style="font-size:0.85em" ><br>&nbsp;@color[yellow](Create a New Project package directory)
<br><br><br>&nbsp;@color[yellow](Create Build Files &lpar;DSC, DEC, and FDF&rpar;)
<br><br><br>&nbsp;@color[yellow](Update target.txt to make your Project the default)
<br><br><br>&nbsp;@color[gray](Use UEFI PI phases to Port all project modules)
<br><br><br>&nbsp;@color[gray](Update DSC w/ new libraries, modules, and PCDs values)
<br><br><br>&nbsp;@color[gray](Minimums for UEFI Shell)</font></span></p>
@snapend



Note:

1. Create a New Project package directory
2. Create Build Files (DSC, DEC, and FDF)
3. Update conf/target.txt to make your Project the default build (optional)  
4. Port all required modules for your project through all UEFI Platform initialization phases
5. Update build text (DSC, DEC, FDF) files with libraries, ported modules, and PCD values to configure modules
6. Minimums for UEFI Shell

<!---  next slide  -->

---?image=/assets/images/slides/Slide39.JPG
@title[New Directory Structure  ]
<p align="right"><span class="gold" ><b>New Directory Structure</b>  </span></p>

Note:

We will start with our example of Minnowboard Max and it's project directory

Copy this directory


---?image=/assets/images/slides/Slide41_1.JPG
<!-- .slide: data-transition="none" -->
@title[Creating a New Project Directory]
<p align="right"><span class="gold" ><b>New Directory Structure </b> </span></p>

Note:
-  The platform package directory contains project files
-  DEC
-  DSC
-  FDF
-  Specific platform directories have files for other functions
-  PEI
-  DXE
-  SMM
-  SIO
-  Setup
-  Library
-  Etc…

Copy the project directory that is working to a new directory

Our example is NewProjectPkg





+++?image=/assets/images/slides/Slide41_2.JPG
<!-- .slide: data-background-transition="none" -->
<!-- .slide: data-transition="none" -->
@title[Creating a New Project Directory 02]
<p align="right"><span class="gold" ><b>New Directory Structure </b> </span></p>

Note:
-  The platform package directory contains project files
-  DEC
-  DSC
-  FDF
-  Specific platform directories have files for other functions
-  PEI
-  DXE
-  SMM
-  SIO
-  Setup
-  Library
-  Etc…


+++?image=/assets/images/slides/Slide41_3.JPG
<!-- .slide: data-background-transition="none" -->
<!-- .slide: data-transition="none" -->
@title[Creating a New Project Directory 03]
<p align="right"><span class="gold" ><b>New Directory Structure  </b></span></p>

Note:
-  The platform package directory contains project files
-  DEC
-  DSC
-  FDF
-  Specific platform directories have files for other functions
-  PEI
-  DXE
-  SMM
-  SIO
-  Setup
-  Library
-  Etc…


+++?image=/assets/images/slides/Slide41_4.JPG
<!-- .slide: data-background-transition="none" -->
<!-- .slide: data-transition="none" -->
@title[Creating a New Project Directory 04]
<p align="right"><span class="gold" ><b>New Directory Structure  </b></span></p>

Note:
-  The platform package directory contains project files
-  DEC
-  DSC
-  FDF
-  Specific platform directories have files for other functions
-  PEI
-  DXE
-  SMM
-  SIO
-  Setup
-  Library
-  Etc…


---?image=/assets/images/slides/Slide42.JPG
<!-- .slide: data-transition="none" -->
@title[PCD Example with New Project ]
<p align="right"><span class="gold" ><b>PCD Example with New Project  </b> </span></p>

Note:

-  PCDs are declared in corresponding Silicon and Chipset Packages, according to how they are used with default values in the package DEC files.

-  PCDs are assigned values in the Project Package DSC file, overriding values in the DEC file.


+++?image=/assets/images/slides/Slide43.JPG
<!-- .slide: data-background-transition="none" -->
<!-- .slide: data-transition="none" -->
@title[PCD Example with New Project 02]
<p align="right"><span class="gold" ><b>PCD Example with New Project   </b></span></p>

Note:

-  PCDs are declared in corresponding Silicon and Chipset Packages, according to how they are used with default values in the package DEC files.

-  PCDs are assigned values in the Project Package DSC file, overriding values in the DEC file.


---?image=assets/images/binary-strings-black2.jpg
<!-- .slide: data-transition="none" -->
@title[Porting Task List Section 04]
<p align="center"><span style="font-size:01.25em"><font color="#e49436"><b>Porting Task List</b></span></p>

@snap[north-east span-90 ]
<br>
<br>
<br>
@box[bg-grey-15 text-white rounded my-box-pad2  ](<p style="line-height:60%" ><span style="font-size:0.9em; font-weight: bold;" > <br><br> <br><br><br><br><br><br><br><br><br><br><br><br><br>&nbsp;</span></p>)
@snapend


@snap[north-east span-15]
![Porting_task_list.gif](/assets/images/tenor.gif)
@snapend

<!---  col of numbers  -->

@snap[north-west span-10 ]
<br>
<br>
<p style="line-height:60%" align="left"><span style="font-size:02.0em" ><font color="#808080"><br>@color[yellow](&#10102;<br><br>&#10103;<br><br>&#10104;<br><br>)@color[red](&#10105;)@color[#808080](<br><br>&#10106;<br><br>&#10107;)  </font></span></p>
@snapend


@snap[north-east span-90 ]
<br>
<br>
<p style="line-height:60%" align="left"><span style="font-size:0.85em" ><br>&nbsp;@color[gray](Create a New Project package directory)
<br><br><br>&nbsp;@color[gray](Create Build Files &lpar;DSC, DEC, and FDF&rpar;)
<br><br><br>&nbsp;@color[gray](Update target.txt to make your Project the default)
<br><br><br>&nbsp;@color[yellow](Use UEFI PI phases to Port all project modules)
<br><br><br>&nbsp;@color[gray](Update DSC w/ new libraries, modules, and PCDs values)
<br><br><br>&nbsp;@color[gray](Minimums for UEFI Shell)</font></span></p>
@snapend



Note:

1. Create a New Project package directory
2. Create Build Files (DSC, DEC, and FDF)
3. Update conf/target.txt to make your Project the default build (optional)  
4. Port all required modules for your project through all UEFI Platform initialization phases
5. Update build text (DSC, DEC, FDF) files with libraries, ported modules, and PCD values to configure modules
6. Minimums for UEFI Shell



+++?image=assets/images/binary-strings-black2.jpg
<!-- .slide: data-background-transition="none" -->
<!-- .slide: data-transition="none" -->
@title[Porting Task List Section 04-2]
<p align="center"><span style="font-size:01.25em"><font color="#e49436"><b>Porting Task List</b></span></p>

@snap[north-east span-90 ]
<br>
<br>
<br>
@box[bg-grey-15 text-white rounded my-box-pad2  ](<p style="line-height:60%" ><span style="font-size:0.9em; font-weight: bold;" > <br><br> <br><br><br><br><br><br><br><br><br><br><br><br><br>&nbsp;</span></p>)
@snapend


@snap[north-east span-15]
![Porting_task_list.gif](/assets/images/tenor.gif)
@snapend

<!---  col of numbers  -->

@snap[north-west span-10 ]
<br>
<br>
<p style="line-height:60%" align="left"><span style="font-size:02.0em" ><font color="#808080"><br>@color[yellow](&#10102;<br><br>&#10103;<br><br>&#10104;<br><br>)@color[red](&#10105;)@color[#808080](<br><br>&#10106;<br><br>&#10107;)  </font></span></p>
@snapend


@snap[north-east span-90 ]
<br>
<br>
<p style="line-height:60%" align="left"><span style="font-size:0.85em" ><br>&nbsp;@color[gray](Create a New Project package directory)
<br><br><br>&nbsp;@color[gray](Create Build Files &lpar;DSC, DEC, and FDF&rpar;)
<br><br><br>&nbsp;@color[gray](Update target.txt to make your Project the default)
<br><br><br>&nbsp;@color[yellow](Use UEFI PI phases to Port all project modules)
<br><br><br>&nbsp;@color[gray](Update DSC w/ new libraries, modules, and PCDs values)
<br><br><br>&nbsp;@color[gray](Minimums for UEFI Shell)</font></span></p>
@snapend

@snap[midpoint span-85 ]
<br>
![boot-flow](/assets/images/boot-flow2.png)
@snapend

@snap[south span-100 fragment]
@box[bg-purple-pp text-white rounded my-box-pad2  ](<p style="line-height:80%"><span style="font-size:0.80em" >Port all required modules for your project using <br>UEFI Platform Initialization phases as a guide<br>&nbsp;</span></p>)
@snapend

Note:

1. Create a New Project package directory
2. Create Build Files (DSC, DEC, and FDF)
3. Update conf/target.txt to make your Project the default build (optional)  
4. Port all required modules for your project through all UEFI Platform initialization phases
5. Update build text (DSC, DEC, FDF) files with libraries, ported modules, and PCD values to configure modules
6. Minimums for UEFI Shell

### This will be the longest task and depending on the project may take several weeks




---?image=/assets/images/slides/Slide24_1.JPG
@title[Platform Initialization: SEC Phase]
<p align="right"><span class="gold" ><b>Platform Initialization: SEC Phase</b></span></p>


@snap[north span-40 fragment]
<br>
<br>
@box[bg-lt-blue-pp text-black my-box-pad2  ](<p style="line-height:40%" align="left"><span style="font-size:0.80em" >@color[white](&nbsp;&nbsp;x86 &lpar;IA32 &amp; x64&rpar;)</span><br><br><span style="font-size:0.50em; font-family:Consolas; " >&nbsp;&nbsp;&nbsp;&nbsp;/MyWorkDir<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  /IA32FamilyCpuPkg<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /SecCore/Ia32<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /ResetVec.asm16<br>&nbsp;&nbsp;</span></p>)
@snapend


@snap[north span-40 fragment]
<br>
<br>
<br>
<br>
<br>
<br>
<br>
@box[bg-gold2 text-black my-box-pad2  ](<p style="line-height:40%" align="left"><span style="font-size:0.80em" >@color[white](&nbsp;&nbsp;Itanium)</span><br><br><span style="font-size:0.50em; font-family:Consolas; " >&nbsp;&nbsp;&nbsp;&nbsp;/MyWorkDir<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  /ItaniumFamilyCpuPkg<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /SecCore/Ipf<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /SecCore.s/ SALE_ENTRY<br>&nbsp;&nbsp;</span></p>)
@snapend

@snap[north span-40 fragment]
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
@box[bg-grey-50 text-black my-box-pad2  ](<p style="line-height:40%" align="left"><span style="font-size:0.80em" >@color[white](&nbsp;&nbsp;Other Arch)</span><br><br><span style="font-size:0.50em; font-family:Consolas; " >&nbsp;&nbsp;&nbsp;&nbsp;/MyWorkDir<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  /XCpuPkg<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /SecCore/Xarch<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;</span></p>)
@snapend



Note:
### SEC phase
-  Minimal code
-  Execute in place (XIP) from flash
-  Execution started by reset vector
-  Enables temp memory for C code (data & stack)
-  Transfers control to PEI


-  Let’s start with the SEC phase.
-  What do we need to be current sermon about in the SEC?
-  We will have Minimal code and we are most likely in assembly language for the particular processor architecture.
-  We will be executing from flash , so this means the code will not be compressed.
-  A point to take especially if you are going to be using a hardware debugger, is we will start Execution at the reset vector
-  It’s job is to Enables temp memory
-  Set up the Data and Stack Cached areas . This sets up our cache as RAM or our cache as no eviction mode.
-  Which will Enable the C Code
-  And then it will finally Transfer control to PEI

### entry point for SEC
-  What we are showing at the right of the slide is the exact location in the EDK II source tree of the reset vector. For X86 Intel architecture all the code will be in the directory Ia32FamilyCpuPkg and the reset vector will be in the file ResetVec.asm16. for this particular file to reset Vector will start to execute the code in this file. There are approximately about three assembly language instructions before it will make a jump into a platform’s ported SEC library source code. This is where we would need to start to port our new platform code.
-  The Middle example is for Itanium and would be similar to the X86 example. In this example there is the SALE_ENTRY.
-  Currently we only have two processor architectures but if we had a third the “OtherArch” example would be where it would be located.



---?image=/assets/images/slides/Slide25_1.JPG
@title[SEC Code Start]
<p style="line-height:80%" align="right"><span class="gold" ><b>SEC Code Start</b><br></span><span style="font-size:0.80em" >@color[white]( - Source Code Example)</span></p>
<p style="line-height:80%" align="left"><span style="font-size:0.90em" >Location for MinnowBoard MAX:<br></span><span style="font-size:0.70em" >&nbsp;&nbsp;&nbsp;&nbsp;`IA32FamilyCpuPkg/SecCore/Ia32/ResetVec.nasmb`</span></p>

@snap[north-west span-35 fragment]
<br>
<br>
<br>
<br>
<br>
<p style="line-height:70%" align="left"><span style="font-size:0.60em" ><br>Entry point&nbsp;&nbsp;<br> </span><span style="font-size:02.25em" >@color[yellow](&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&rdca;)</span></p>
@snapend


@snap[south-west span-20 fragment]
<p style="line-height:70%" align="left"><span style="font-size:0.60em" >Binary of the compiled Firmware image at 4GB<br><br> </span>
<span style="font-size:02.25em" >@color[yellow](&nbsp;&nbsp;&nbsp;&rdca;)</span><br>&nbsp;</p>


@snapend

Note:

Example: IA32FamilyCpuPkg/SecCore/Ia32/ResetVec.nasmb
<pre>
;
; For IA32, the reset vector must be at 0xFFFFFFF0, i.e., 4G-16 byte
; Execution starts here upon power-on/platform-reset.
;
ResetHandler:
    nop
    nop
ApStartup:
    ;
    ; Jmp Rel16 instruction
    ; Use machine code directly in case of the assembler optimization
    ; SEC entry point relatvie address will be fixed up by some build tool.
    ;
    ; Typically, SEC entry point is the function _ModuleEntryPoint() defined in
    ; SecEntry.asm
    ;
    DB      0e9h
    DW      -3

</pre>


---
@title[Platform SEC Lib for MinnowBoard MAX]
<p align="right"><span class="gold" ><b>Platform SEC Lib for MinnowBoard MAX</b></span></p>

@snap[north-west span-100 ]
<br>
<br>
<br>

@box[bg-gold2 text-white rounded my-box-pad2  ](<p style="line-height:60%" ><span style="font-size:0.9em; font-weight: bold;" > <br><br><br> <br><br><br><br><br><br><br><br><br><br><br><br><br>&nbsp;</span></p>)
@snapend

@snap[north-west span-100 ]
<br>
<br>
<br>
<p style="line-height:75%" align="left"><span style="font-size:0.75em; font-family:Consolas; ;color:black" ><br>&nbsp; &nbsp; 
&nbsp;NewProjectPkg/<br>&nbsp; &nbsp; 
&nbsp;&nbsp;&nbsp; Library/<br>&nbsp; &nbsp; 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    PlatformSecLib/<br>&nbsp; &nbsp; 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    PlatformSecLib.c<br>&nbsp; &nbsp; 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    PlatformSecLib.h<br>&nbsp; &nbsp; 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    PlatformSecLib.inf<br>&nbsp; &nbsp; 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    IA32/<br>&nbsp; &nbsp; 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#0558ff">     	Chipset.inc<br>&nbsp; &nbsp; 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;		Flat32.asm<br>&nbsp; &nbsp; 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;		Platform.inc<br>&nbsp; &nbsp; 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;		SecCore.inc<br>&nbsp; &nbsp; 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;		Ia32.inc<br>&nbsp; <br>&nbsp; </font>
</span></p>
@snapend

@snap[north-east span-50 fragment]
<br>
<br>
<br>
<br>
<br>
<p style="line-height:70%" align="left"><span style="font-size:0.80em; ;color:green" ><br><br><br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<b>`_ModuleEntryPoint` or <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`Flat32Start`</b><br><br><br> </span>
<span style="font-size:03.25em" >@color[red](<b>&ldca;</b>)</span><br>&nbsp;</p>
@snapend


Note:

-  Entry point after reset vector is platform specific
  -  SecEntry.asm
  -  ModuleEntryPoint
-  SecNewProject.asm calls entry for setting up temporary memory and APs
  -  SecPlatformInitTram
  -  SecPlatformApEntryPoint
-  SecCPU.Asm sets cache for no eviction mode
  -  CPU & MTRR register defines
  -  Ia32.inc
-  NewProjectSecLib.c SEC platform main (i.e. enable FWH decode)

-  Of this slide we have what we need to port our new package platform for the SEC  phase.
-  We find this code in our new platform package directory under the library directory under the directory called something like new platform SEC lib. Under this directory we see that we have a “C”, “H” and Inf files, And we also see another directory, in our case for our example platform, we have an IA32 directory. This directory would have assembly language source files for our port.

-  Let’s take a look at the details of these files:
  -  After the reset vector and after those initial architecture specific instructions, a jump will be made into the new platform SEC library code. The Entry point after common reset vector is platform specific in SecEntry.asm  with the label ModuleEntryPoint.

-  The file SecNewProject.asm – calls the entry for setting up our temporary memory and the Application Processors
-  We will need to look at the code at the label SecPlatformInitTram where we would  make a call to set up our temporary memory. Probably the cache as RAM. But, it could be something different.
-  The label SecPlatformApEntryPoint is where we be setting up the entry point for our application processors.
-  The file SecCPU.Asm – is the actual code that Sets the Cache for no eviction mode or cache as RAM.
-  The include file  Ia32.inc – has Defines for the MTRR registers and processor specific defines  

-  Finally, the C. source code file NewProjectSecLib.c – and this file would have the Sec Platform MAIN entry– and it would be responsible for things like to Enable FWH decoding etc.





---?image=/assets/images/slides/Slide56.JPG
@title[Temporary Memory Example]
<p align="right"><span class="gold" ><b>Temporary Memory Example</b></span></p>


Note:
-  This is an example!!!!!

-  SEC PCDs used to set up temp RAM size and location
  -  PcdTemporaryRamSize
  -  PcdTemporaryRamBase



---?image=/assets/images/slides/Slide28_1.JPG
@title[SEC Lib, PCD Example ]
<!---  PCD Example   -->
<p align="right"><span class="gold" ><b>SEC Lib, PCD Example</b> </span></p>


@snap[north-east span-90 fragment]
<p align="left" style="line-height:40%"><span style="font-size:0.8em; ">
<br>
<br>
<br>
Defined in Package DEC @color[yellow](`NewProjectPkg.dec`)</span></p>
@box[bg-black text-white my-box-pad2  ](<p style="line-height:40%" align="left"><span style="font-size:0.450em; font-family:Consolas; " >&nbsp;&nbsp;[PcdsFixedAtBuild]<br>&nbsp;&nbsp;gPlatformModulePkgTokenSpaceGuid.@color[red](PcdFlashMicroCodeAddress)|0xFFFF0000|UINT32|0x20x&nbsp;&nbsp;</span></p>)
@snapend

@snap[north-east span-90 fragment]
<br>
<p align="left" style="line-height:40%"><span style="font-size:0.8em; ">
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
Module INF lists which PCDs get accessed</span></p>
@box[bg-black text-white my-box-pad2  ](<p style="line-height:40%" align="left"><span style="font-size:0.450em; font-family:Consolas; " >&nbsp;&nbsp;NewProjectPkg/Library/PlatformSecLib/PlatformSecLib.inf<br>&nbsp;&nbsp;[Pcd]<br>&nbsp;&nbsp;gPlatformModulePkgTokenSpaceGuid.@color[red](PcdFlashMicroCodeAddress) <br>&nbsp;&nbsp;</span></p>)
@snapend


@snap[north-east span-90 fragment]
<br>
<br>
<br>
<p align="left" style="line-height:40%"><span style="font-size:0.8em; "><br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>Value to use in Project @color[yellow](`NewProjectPkg.dsc`) </span></p>
@box[bg-black text-white my-box-pad2  ](<p style="line-height:40%" align="left"><span style="font-size:0.450em; font-family:Consolas; " >&nbsp;&nbsp;[PcdsFixedAtBuild]<br>&nbsp;&nbsp;gPlatformModulePkgTokenSpaceGuid.@color[red](PcdFlashMicroCodeAddress)|<font color="cyan">0xfff90000</font><br>&nbsp;&nbsp;</span></p>)
@snapend


@snap[north-east span-90 fragment]
<br>
<br>
<br>
<br>
<p align="left" style="line-height:40%"><span style="font-size:0.8em; "><br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
SEC - Referenced in the SEC library code </span></p>
@box[bg-black text-white my-box-pad2  ](<p style="line-height:40%" align="left"><span style="font-size:0.450em; font-family:Consolas; " >&nbsp;&nbsp;NewProjectPkg/Library/PlatformSecLib/Ia32/flat.asm<br>&nbsp;&nbsp; ; Get the Flash Microcode address<br>&nbsp;&nbsp; mov     esi, PcdGet32 (@color[red](PcdFlashMicroCodeAddress))<br>&nbsp;&nbsp;&nbsp;&nbsp;</span></p>)
<br>
@snapend




Note:
-  SEC PCDs used to set up temp RAM size and location
  -  PcdTemporaryRamSize
  -  PcdTemporaryRamBase



---?image=/assets/images/slides/Slide29_1.JPG
<!-- .slide: data-transition="none" -->
@title[PEI Phase ]
<p align="right"><span class="gold" ><b>PEI Phase</b> </span></p>

@snap[north-east span-80 fragment]
<br>
<p align="left" style="line-height:40%"><span style="font-size:0.8em; "><br></span></p>
@box[bg-royal text-white rounded my-box-pad2  ](<p style="line-height:70%"><span style="font-size:0.8em; " >Main platform PEI code is in `PlatformPei` and `PlatformInitPei`<br>&nbsp;&nbsp;</span></p>)
@snapend



@snap[north-east span-80 fragment]
<br>
<br>
<br>
<br>
<p align="left" style="line-height:40%"><span style="font-size:0.8em; "><br><br><br></span></p>
@box[bg-green-pp text-white rounded my-box-pad2  ](<p style="line-height:70%"><span style="font-size:0.8em; " >PEI code is dependent on the PEI drivers<br>&nbsp;&nbsp;</span></p>)
@snapend

@snap[north-east span-80 fragment]
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<p align="left" style="line-height:40%"><span style="font-size:0.8em; "><br></span></p>
@box[bg-gold2 text-white rounded my-box-pad2  ](<p style="line-height:70%"><span style="font-size:0.8em; " >Platform PEI code can be divided into 3 phases<br>&nbsp;&nbsp;</span></p>)
@snapend 

@snap[north-east span-50 fragment]
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<p align="left" style="line-height:40%"><span style="font-size:0.8em; "><br><br><br></span></p>
<p align="left" style="line-height:70%"><span style="font-size:0.7em; ">
@size[2.5](@color[#00ffff](&#10122;))&nbsp;&nbsp;Pre-Memory Initialization<br>
@size[2.5](@color[yellow](&#10123;))&nbsp;&nbsp;Memory Initialization &lpar;MRC&rpar;<br>
@size[2.5](@color[#87E2A9](&#10124;))&nbsp;&nbsp;Post-Memory Initialization
<br>&nbsp;</span></p>

@snapend 

@snap[south-west span-100 fragment]
<p align="left" style="line-height:40%"><span style="font-size:0.8em; "><br></span></p>
@box[bg-purple-pp text-white rounded my-box-pad2  ](<p style="line-height:70%"><span style="font-size:0.9em; " ><b>TIP :</b> Check the DSC file for the PEI Modules used<br>&nbsp;&nbsp;</span></p>)
@snapend 



Note:
-  The main platform PEI code is in a subdirectory of the platform package. (PlatformPei)
-  It references PEIMs in other packages
-  PEI code is dependant on the PEI drivers for the platform for communication to the devices


-  Determine boot mode
  -  S3 and S5 are the most common modes
  -  Recovery mode
-  Low-level initialization of the platform
  -  Find FVs that contain DXE
-  Discover and initialize main memory
-  Transfer control according to boot mode
  -  If S5 hands control to DXE
  -  If S3 uses waking vector


-  Platform PEI code can be divided into 3 phases:
  1.  Pre-Memory Initialization
    -  Initialize the memory controller
    -  Detect boot mode.
    -  Detect video adapter
  2.  Memory Initialization (MRC)
    -  Install  UEFI Memory.
    -  Capsule coalesce, Capsule Boot.
    -  Create HOB of system memory.
  3.  Post-Memory initialization
    -  PCH initialization after MRC.
    -  SIO initialization.
    - Install ResetSystem and FinvFv PPI, if  recovery boot mode.
    - Set MTRR for PEI
    - Create FV HOB and Flash HOB
    - Install RecoveryModule and AtaController PPI  if  recovery boot mode.


---?image=/assets/images/slides/Slide29_1.JPG
@title[PEI Phase – MAX has 2 PEIM Modules 01]
<p align="right"><span class="gold" ><b>PEI Phase – MAX has 2 PEIM Modules </b></span></p>
@snap[north-east span-85 ]
<br>
<p align="left" style="line-height:40%"><span style="font-size:0.8em; "><br></span></p>
@box[bg-black text-white rounded my-box-pad2  ](<p style="line-height:50%"><span style="font-size:0.8em; " ><br><br><br><br><br><br><br><br><br><br><br><br><br><br>&nbsp;&nbsp;</span></p>)
@snapend

@snap[north-east span-80 ]
<br>
<p align="left" style="line-height:40%"><span style="font-size:0.8em; "><br></span></p>
<p align="left" style="line-height:60%"><span style="font-size:0.65em; font-family:Consolas;  " >
NewProjectPkg/<br>
&nbsp;&nbsp;     @color[cyan]( . . .)<br><br>
PlatformInitPei/<br>
&nbsp;&nbsp; @color[red](PlatformEarlyInit.inf)<br>
&nbsp;&nbsp; BootMode.c<br>
&nbsp;&nbsp; CpuInitPeim.c<br>
&nbsp;&nbsp; PchInitPeim.c<br>
&nbsp;&nbsp; MchInit.c<br>
&nbsp;&nbsp; MemoryCallback.c<br>
&nbsp;&nbsp; MemoryPeim.c<br>
<br>&nbsp;&nbsp;</span></p>
@snapend


@snap[north-east span-45 ]
<br>
<p align="left" style="line-height:40%"><span style="font-size:0.8em; "><br></span></p>
<p align="left" style="line-height:60%"><span style="font-size:0.65em;  font-family:Consolas; " >
&nbsp;&nbsp;   @color[cyan](   . . .)<br><br>
&nbsp;&nbsp; PlatformEarlyInit.c<br>
&nbsp;&nbsp; PlatformEarlyInit.h<br>
&nbsp;&nbsp; PlatformInfoInit.c<br>
&nbsp;&nbsp; LegacySpeaker.c<br>
&nbsp;&nbsp; LegacySpeaker.h<br>
&nbsp;&nbsp; Stall.c<br>
&nbsp;&nbsp; PowerFailureHandle.c<br>
&nbsp;&nbsp; PlatformSsaInitPeim.c<br>
&nbsp;&nbsp; IsctWakeReason.c<br> 
<br>&nbsp;&nbsp;</span></p>
@snapend


@snap[south-east span-85 fragment]
<p align="left" style="line-height:40%"><span style="font-size:0.8em; "><br></span></p>
@box[bg-blue-pp text-white rounded my-box-pad2  ](<p align="left" style="line-height:50%"><span style="font-size:0.45em; color:yellow " >&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@size[01.9em](<b>NewProject.DSC file: </b>)<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`[Components.IA32]`<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`NewProject/PlatformInitPei/PlatformEarlyInit.inf`<br>&nbsp;&nbsp;</span></p>)
@snapend 

Note:
-   The main platform PEI code is in a subdirectory of the platform package. (PlatformPei)
-  It references PEIMs in other packages
-  PEI code is dependant on the PEI drivers for the platform for communication to the devices



---?image=/assets/images/slides/Slide29_1.JPG
@title[PEI Phase – MAX has 2 PEIM Modules 02]
<p align="right"><span class="gold" ><b>PEI Phase – MAX has 2 PEIM Modules</b> </span></p>

@snap[north-east span-85 ]
<br>
<p align="left" style="line-height:40%"><span style="font-size:0.8em; "><br></span></p>
@box[bg-black text-white rounded my-box-pad2  ](<p style="line-height:50%"><span style="font-size:0.8em; " ><br><br><br><br><br><br><br><br><br><br><br><br><br><br>&nbsp;&nbsp;</span></p>)
@snapend

@snap[north-east span-60 ]
<br>
<p align="left" style="line-height:40%"><span style="font-size:0.8em; "><br></span></p>
<p align="left" style="line-height:60%"><span style="font-size:0.65em; font-family:Consolas;  " >
NewProjectPkg/<br>
&nbsp;&nbsp;     @color[cyan]( . . .)<br><br>
PlatformPei/<br>
&nbsp;&nbsp; @color[red]( PlatformPeiBB.inf)<br>
&nbsp;&nbsp; Platform.c<br>
&nbsp;&nbsp; Platform.h<br>
&nbsp;&nbsp; MemoryCallback.c<br>
&nbsp;&nbsp; CommonHeader.h<br>
&nbsp;&nbsp; Stall.c<br>
&nbsp;&nbsp; BootMode.c<br>
<br>&nbsp;&nbsp;</span></p>
@snapend




@snap[south-east span-85 fragment]
<p align="left" style="line-height:40%"><span style="font-size:0.8em; "><br></span></p>
@box[bg-blue-pp text-white rounded my-box-pad2  ](<p align="left" style="line-height:50%"><span style="font-size:0.45em; color:yellow " >&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@size[01.9em](<b>NewProject.DSC file: </b>)<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`[Components.IA32]`<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`NewProject/PlatformPei/PlatformBB.inf`<br>&nbsp;&nbsp;</span></p>)
@snapend 


Note:
-   The main platform PEI code is in a subdirectory of the platform package. (PlatformPei)
-  It references PEIMs in other packages
-  PEI code is dependant on the PEI drivers for the platform for communication to the devices



---?image=/assets/images/slides/Slide75.JPG
@title[Recommended PEI Addresses]
<p align="right"><span class="gold" >@size[01.25em](<b>Recommended PEI Addresses</b> )</span></p>

Note:

-  Platform information commonly used in PEI
  -  Base addresses
  -  GPIO addresses
  -  SMBUS address
  -  Memory configuration (channels, ports, etc…)
  -  ACPI settings (base address register, etc…)
-  Goal is to extract these concepts in PCD entries and make them changeable through DSC without having to modify module source



---?image=/assets/images/slides/Slide77.JPG
@title[How to search Workspace]
<p align="right"><span class="gold" ><b>How to search for Addresses in the Workspace</b></span></p>

Note:

-  How to search for GPIOs for NewProjectPkg 
 -    KEY - search the workspace for a string and work back to Data structures declaring then use the DSC for which modules are included


---?image=/assets/images/slides/Slide79.JPG
<!-- .slide: data-transition="none" -->
@title[How to search for GPIOs for NewProjectPkg]
<p align="right"><span class="gold" ><b>How to search for GPIOs for NewProjectPkg</b></span></p>



+++?image=/assets/images/slides/Slide80.JPG
<!-- .slide: data-background-transition="none" -->
<!-- .slide: data-transition="none" -->
@title[How to search for GPIOs for NewProjectPkg 02]
<p align="right"><span class="gold" ><b>How to search for GPIOs for NewProjectPkg</b></span></p>

Note:


+++?image=/assets/images/slides/Slide81.JPG
<!-- .slide: data-background-transition="none" -->
<!-- .slide: data-transition="none" -->
@title[How to search for GPIOs for NewProjectPkg 03]
<p align="right"><span class="gold" ><b>How to search for GPIOs for NewProjectPkg</b></span></p>

Note:


+++?image=/assets/images/slides/Slide82.JPG
<!-- .slide: data-background-transition="none" -->
<!-- .slide: data-transition="none" -->
@title[How to search for GPIOs for NewProjectPkg 04]
<p align="right"><span class="gold" ><b>How to search for GPIOs for NewProjectPkg</b></span></p>

Note:


+++?image=/assets/images/slides/Slide83.JPG
<!-- .slide: data-background-transition="none" -->
<!-- .slide: data-transition="none" -->
@title[How to search for GPIOs for NewProjectPkg 05]
<p align="right"><span class="gold" ><b>How to search for GPIOs for NewProjectPkg</b></span></p>

Note:




---?image=/assets/images/slides/Slide28_1.JPG
@title[PEI Memory Base Address, PCD Example ]
<!---  PCD Example   -->
<p align="right"><span class="gold" ><b>PEI Memory Base Address, PCD Example</b> </span></p>


@snap[north-east span-90 fragment]
<p align="left" style="line-height:40%"><span style="font-size:0.8em; ">
<br>
<br>
<br>
Defined in Package DEC @color[yellow](`NewProjectPkg.dec`)</span></p>
@box[bg-black text-white my-box-pad2  ](<p style="line-height:40%" align="left"><span style="font-size:0.450em; font-family:Consolas; " >&nbsp;&nbsp;[PcdsFixedAtBuild]<br>&nbsp;&nbsp;gEfiIchPkgTokenSpaceGuid.@color[red](PcdPeiIchEhciControllerMemoryBaseAddress)|0|UINT32|0x03x&nbsp;&nbsp;</span></p>)
@snapend

@snap[north-east span-90 fragment]
<br>
<p align="left" style="line-height:40%"><span style="font-size:0.8em; ">
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
Module INF lists which PCDs get accessed</span></p>
@box[bg-black text-white my-box-pad2  ](<p style="line-height:40%" align="left"><span style="font-size:0.450em; font-family:Consolas; " >&nbsp;&nbsp;PlatformInitPei/PlatformEarlyInit.inf<br>&nbsp;&nbsp;[Pcd]<br>&nbsp;&nbsp;gEfiIchTokenSpaceGuid.@color[red](PcdPeiIchEhciControllerMemoryBaseAddress) <br>&nbsp;&nbsp;</span></p>)
@snapend


@snap[north-east span-90 fragment]
<br>
<br>
<br>
<p align="left" style="line-height:40%"><span style="font-size:0.8em; "><br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>Value to use in Project @color[yellow](`NewProjectPkg.dsc`) </span></p>
@box[bg-black text-white my-box-pad2  ](<p style="line-height:40%" align="left"><span style="font-size:0.450em; font-family:Consolas; " >&nbsp;&nbsp;[PcdsFixedAtBuild]<br>&nbsp;&nbsp;gEifIchTokenSpaceGuid.@color[red](PcdPeiIchEhciControllerMemoryBaseAddress)|<font color="cyan">0xFC000000</font><br>&nbsp;&nbsp;</span></p>)
@snapend


@snap[north-east span-90 fragment]
<br>
<br>
<br>
<br>
<p align="left" style="line-height:40%"><span style="font-size:0.8em; "><br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
PEI - Referenced in the PEI code </span></p>
@box[bg-black text-white my-box-pad2  ](<p style="line-height:40%" align="left"><span style="font-size:0.450em; font-family:Consolas; " >&nbsp;&nbsp;/PlatformInitPei/PchInitPeim.c &nbsp;&nbsp;&nbsp;&nbsp;  InstallPeiPchUsbPolicy&lpar;&rpar;<br>&nbsp;&nbsp; &nbsp;&nbsp;PeiPchUsbPolicyPpi-&gt;EhciMemBaseAddr = <br>&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp; PcdGet32&lpar;@color[red](PcdPeiIchEhciControllerMemoryBaseAddress)&rpar;;<br>&nbsp;&nbsp;&nbsp;&nbsp;</span></p>)
<br>
@snapend




Note:
Lets take a look at a PEI PCD example

Here we see that we are using the PEI Memory Base Address for PeiIchEhciControllerMemoryBaseAddress

It IS Defined in ICH X Package DEC
- [PcdsFixedAtBuild] 
  - gEfiIchTokenSpaceGuid.PcdPeiIchEhciControllerMemoryBaseAddress|0|UINT32|0x39

The Module INF lists which PCDs get accessed in the 
  PlatformInitPei/PlatformEarlyInit.inf
- [Pcd]   
  - gEfiIchTokenSpaceGuid.PcdPeiIchEhciControllerMemoryBaseAddress

The Value to use is in the Project New Package DSC
	[PcdsFixedAtBuild]
     gEfiIchTokenSpaceGuid.PcdPeiIchEhciControllerMemoryBaseAddress|0xFC000000

The example in the code:
PEI - Referenced in the PEI code -    /PlatformInitPei/PchInitPeim.c    in function  InstallPeiPchUsbPolicy()
  -   PeiPchUsbPolicyPpi->EhciMemBaseAddr = 
    -    PcdGet32(PcdPeiIchEhciControllerMemoryBaseAddress);


---?image=/assets/images/slides/Slide91.JPG
@title[Critical PEIMs]
<p align="right"><span class="gold" ><b>Critical PEIMs  </b></span></p>


Note:
-  So what are the Critical PEIMs?


-  These are the minimum set of PEI components that must be dispatched during the PEI.
-  The list here is those PEIMs that encapsulate those. The order shown here is not the dispatch order.  The DXE IPL PEIM is dispatched last
-  The CPU PEIM installs the CPU_IO PPI that provides CPU IO functions
-  The DXE IPL PEIM hands off control from the PEI Core to DXE
-  The PCI PEIM provides basic PCI functions to PEI
-  The Stall PEIM provides a sleep or wait function
-  The Status Code PEIM is for debug messages (Port80) and serial port if in debug mode
-  The SMBUS PEIM initializes and provides SMBUS access
-  The Memory Control PEIMs read the SPD and initialize/configure memory

-  Additional platform PEIMs for flash map layout, boot policy determination, fan control and misc chipset initialization
-  Platform Configurations Database PCD



-  Porting Key with respect to the Copied Project/platform
  -  The ones in green will typically not require changes if your platform is PCAT based.
  -  The ones in orange  will need attention if your platform is different that the reference platforms.



---?image=/assets/images/slides/Slide41_X.JPG
@title[Initial Program Load (IPL) PEIM for DXE]
<p align="right"><span class="gold" ><b>Initial Program Load (IPL) PEIM for DXE </b> </span></p>
<br>
<div class="left">
<span style="font-size:0.8em" > &nbsp;</span>
</div>
<div class="right">
<br>
@ul[no-bullet]
-  <font color="#FFFF00">&nbsp;&nbsp;<b>Creates HOBs </b></font> <br><br>
-  <font color="white">&nbsp;&nbsp;<b>Locates DXE main </b></font>  <BR><br>
-  <font color="#ffc000">&nbsp;&nbsp;<b>Switch Stacks</b></font>  <br><br>
-  <font color="cyan">&nbsp;&nbsp;<b>&rarr;&nbsp;DxeMain() </b></font> 
@ulend
</div>			

Note:
-  The DXE IPL PEIM should not require porting, but  knowing what is does it important.  This is a good place for a breakpoint and starting to debug.  For example, if porting didn’t work this is where it will fail.

-  The DXE IPL PEIM performs several tasks

-  Shadows DXE IPL into permanent memory to allow sharing of the decompression algorithm and several other library routines (e.g. security)
-  Allocates 128KB of stack for the DXE phase
-  Creates HOBs for passing library routines and the firmware volumes discovered during the PEI phase. Most commonly this is the main FV and any other FVs that DXE will use to load drivers from (for example backup block)
-  If S3, then the OS waking vector is called
-  Locate DXE Main in the FVs
-  If not S3 then switch stacks and call DXE Main


-  The last PEIM to execute
-  Shadows into permanent memory
-  Shares data from PEI phase with DXE
-  Creates a stack for DXE Phase
-  Creates HOBs
-  Calls S3 vector if appropriate
-  Locate DXE Main
-  Switch stack and call DXE Main



---?image=/assets/images/slides/Slide42_1.JPG
@title[DXE Phase]
<p align="center"><span class="gold" ><b>DXE Phase</b> </span></p>
<div class="left-1">
<span style="font-size:0.8em" > &nbsp;</span>
</div>
<div class="right-1">
<br>
<br>
<ul style="list-style-type:none">
  <li><span style="font-size:0.9em" ><font color="yellow"> Main platform DXE code in subdirectories of the platform package containing “DXE” in the name</font> </span></li><br>
  <li><span style="font-size:0.9em" ><font color="cyan">Establish Architectural Protocols </font> </span></li><br>
  <li><span style="font-size:0.9em" ><font color="#ffc000">Install any required DXE / UEFI Drivers </font> </span></li>
</ul>
</div>		

Note:

-  The main platform DXE code is in subdirectories of the platform package having “DXE” in the directory name (i.e. PciPlatformDxe)
   -  It will reference other packages DXE modules
-  Establish the architectural protocols
  -  Isolate platform specific hardware (e.g., RTC)
  -  Provide support for boot and runtime services
  -  Low level protocols that support DXE APIs
  -  Directly called by DXE core
-  Install any required DXE and then the UEFI Drivers


---?image=/assets/images/slides/Slide99.JPG
@title[DXE Architectural Protocols ]
<p align="right"><span class="gold" ><b>DXE Architectural Protocols (AP)</b></span></p>


Note:

-  Isolate platform specific hardware (e.g., RTC)
-  Provide support for boot and runtime services
-  Low level protocols that support DXE APIs



---?image=/assets/images/slides/Slide101.JPG
@title[How to Search for AP Modules  top]
<p align="right"><span class="gold" ><b>How to Search for AP Modules </b></span></p>



---?image=/assets/images/slides/Slide103.JPG
<!-- .slide: data-transition="none" -->
@title[How to Search for AP Modules 01 ]
<p align="right"><span class="gold" ><b>How to Search for AP Modules in the Project </b></span></p>

Note:
-  Search the Work Space .INF files  for the Architectural Protocols  - key word “Produces”
  -  gEfiCpuArchProtocolGuid 
<pre>
 UefiCpuPkg/CpuDxe/				##PRODUCES
 Vlv2DeviceRefCodePkg/ValleyView2Soc/CPU/CpuInit/Dxe/
 IA32FamilyCpuPkg/CpuArchDxe	##PRODUCES
</pre>

-  Find which module Install the protocol (.i.e Search .c )
  -  gEfiCpuArchProtocolGuid 
-  Check the NewProjectPkg .DSC to see which .INF is included in the [Components] section
-  Vlv2DeviceRefCodePkg/ValleyView2Soc/CPU/CpuInit/Dxe/MpCpu.inf




+++?image=/assets/images/slides/Slide104.JPG
<!-- .slide: data-background-transition="none" -->
<!-- .slide: data-transition="none" -->
@title[How to Search for AP Modules 02 ]
<p align="right"><span class="gold" ><b>How to Search for AP Modules in the Project </b></span></p>

Note:
-  Search the Work Space .INF files  for the Architectural Protocols  - key word “Produces”
  -  gEfiCpuArchProtocolGuid 
<pre>
 UefiCpuPkg/CpuDxe/				##PRODUCES
 Vlv2DeviceRefCodePkg/ValleyView2Soc/CPU/CpuInit/Dxe/
 IA32FamilyCpuPkg/CpuArchDxe	##PRODUCES
</pre>

-  Find which module Install the protocol (.i.e Search .c )
  -  gEfiCpuArchProtocolGuid 
-  Check the NewProjectPkg .DSC to see which .INF is included in the [Components] section
-  Vlv2DeviceRefCodePkg/ValleyView2Soc/CPU/CpuInit/Dxe/MpCpu.inf


+++?image=/assets/images/slides/Slide105.JPG
<!-- .slide: data-background-transition="none" -->
<!-- .slide: data-transition="none" -->
@title[How to Search for AP Modules 03 ]
<p align="right"><span class="gold" ><b>How to Search for AP Modules in the Project </b></span></p>

Note:
-  Search the Work Space .INF files  for the Architectural Protocols  - key word “Produces”
  -  gEfiCpuArchProtocolGuid 
<pre>
 UefiCpuPkg/CpuDxe/				##PRODUCES
 Vlv2DeviceRefCodePkg/ValleyView2Soc/CPU/CpuInit/Dxe/
 IA32FamilyCpuPkg/CpuArchDxe	##PRODUCES
</pre>

-  Find which module Install the protocol (.i.e Search .c )
  -  gEfiCpuArchProtocolGuid 
-  Check the NewProjectPkg .DSC to see which .INF is included in the [Components] section
-  Vlv2DeviceRefCodePkg/ValleyView2Soc/CPU/CpuInit/Dxe/MpCpu.inf


+++?image=/assets/images/slides/Slide106.JPG
<!-- .slide: data-background-transition="none" -->
<!-- .slide: data-transition="none" -->
@title[How to Search for AP Modules 04 ]
<p align="right"><span class="gold" ><b>How to Search for AP Modules in the Project </b></span></p>

Note:
-  Search the Work Space .INF files  for the Architectural Protocols  - key word “Produces”
  -  gEfiCpuArchProtocolGuid 
<pre>
 UefiCpuPkg/CpuDxe/				##PRODUCES
 Vlv2DeviceRefCodePkg/ValleyView2Soc/CPU/CpuInit/Dxe/
 IA32FamilyCpuPkg/CpuArchDxe	##PRODUCES
</pre>

-  Find which module Install the protocol (.i.e Search .c )
  -  gEfiCpuArchProtocolGuid 
-  Check the NewProjectPkg .DSC to see which .INF is included in the [Components] section
-  Vlv2DeviceRefCodePkg/ValleyView2Soc/CPU/CpuInit/Dxe/MpCpu.inf


---?image=/assets/images/slides/Slide78_1.JPG
@title[Location of APs for MAX]
<p align="right"><span class="gold" ><b>Location of Architectural Protocols for MAX</b></span></p>


Note:
- gEfiBdsArchProtocolGuid 	MdeModulePkg/Universal/BdsDxe/ 
- gEfiCapsuleArchProtocolGuid 	MdeModulePkg/Universal/CapsuleRuntimeDxe 
- gEfiCpuArchProtocolGuid                       	Vlv2DeviceRefCodePkg/ValleyView2Soc/CPU/CpuInit/Dxe/MpCpu
- gEfiMetronomeArchProtocolGuid 	Vlv2TbltDevicePkg/Metronome
- gEfiMonotonicCounterArchProtocolGuid 	MdeModulePkg/Universal/MonotonicCounterRuntimeDxe 
- gEfiRealTimeClockArchProtocolGuid 	PcAtChipsetPkg/PcatRealTimeClockRuntimeDxe
- gEfiResetArchProtocolGuid 	Vlv2DeviceRefCodePkg/ValleyView2Soc/SouthCluster/Reset/RuntimeDxe/ 
- gEfiRuntimeArchProtocolGuid 	MdeModulePkg/Core/RuntimeDxe 
- gEfiSecurityArchProtocolGuid 	MdeModulePkg/Universal/SecurityStubDxe
- gEfiStatusCodeRuntimeProtocolGuid 	MdeModulePkg/Universal/ReportStatusCodeRouter/RuntimeDxe 
- gEfiTimerArchProtocolGuid 	Vlv2DeviceRefCodePkg/ValleyView2Soc/SouthCluster/ SmartTimer/Dxe
- gEfiVariableArchProtocolGuid 	MdeModulePkg/Universal/Variable 
- gEfiVariableWriteArchProtocolGuid 	MdeModulePkg/Universal/Variable/RuntimeDxe 
- gEfiWatchdogTimerArchProtocolGuid 	MdeModulePkg/Universal/WatchdogTimerDxe 




---
<!-- .slide: data-transition="none" -->
@title[Platform-Dependent DXE Drivers ]
<p align="right"><span class="gold" ><b>Platform-Dependent DXE Drivers<b></span></p>


@snap[north-west span-100 fragment]
<br>
<p style="line-height:70%" align="left" ><span style="font-size:0.9em; font-weight: bold;" >@color[cyan](Host Bridge Driver)</span></p>
@box[bg-lt-blue-pp text-white rounded my-box-pad2  ](<p style="line-height:40%" align="left" ><span style="font-size:0.450em; font-family:Consolas; " >&nbsp;&nbsp;&nbsp;&nbsp; NewProjectPkg/PciPlatformDxe/PciPlatform.c<br>&nbsp;&nbsp;&nbsp;&nbsp; &lt;@color[yellow](Memory Controller North)&gt;Pkg/PciHostBridgeDxe/<br>&nbsp;</span></p>)
<br>
@snapend


@snap[north-west span-100 fragment]
<br>
<br>
<p style="line-height:50%" ><br><br><br><br>&nbsp;</p>
<p style="line-height:70%" align="left" ><span style="font-size:0.9em; font-weight: bold;" >@color[#87E2A9](PCH Initialize Driver)</span></p>
@box[bg-green2 text-white rounded my-box-pad2  ](<p style="line-height:40%" align="left" ><span style="font-size:0.450em; font-family:Consolas; " >&nbsp;&nbsp;&nbsp;&nbsp; NewProjectPkg/LegacyBiosDxe/Platform.c<br>&nbsp;&nbsp;&nbsp;&nbsp; &lt;@color[yellow](I/O Controller South)&gt;Pkg/PchInitDxe/<br>&nbsp;</span></p>)
<br>
@snapend


@snap[north-west span-100 fragment]
<br>
<br>
<br>
<br>
<br>
<br>
<p style="line-height:50%" ><br><br><br><br>&nbsp;</p>
<p style="line-height:70%" align="left" ><span style="font-size:0.9em; font-weight: bold;" >@color[#00b0f0](SATA Controller Driver)</span></p>
@box[bg-royal text-white rounded my-box-pad2  ](<p style="line-height:40%" align="left" ><span style="font-size:0.450em; font-family:Consolas; " >&nbsp;&nbsp;&nbsp;&nbsp;&lt;@color[yellow](I/O Controller South)&gt;Pkg/SataConrollerDxe/PchSataController<br>&nbsp;</span></p>)
<br>
@snapend



@snap[north-west span-100 fragment]
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<p style="line-height:50%" ><br><br><br><br>&nbsp;<br>&nbsp;</p>
<p style="line-height:70%" align="left" ><span style="font-size:0.9em; font-weight: bold;" >@color[gray](Super I/O Driver)</span></p>
@box[bg-grey-50 text-white rounded my-box-pad2  ](<p style="line-height:40%" align="left" ><span style="font-size:0.450em; font-family:Consolas; " >&nbsp;&nbsp;&nbsp;&nbsp; &lt;@color[yellow](XSioXVer)&gt;Pkg/XSioXVerDxe/<br>&nbsp;</span></p>)
<br>
@snapend


@snap[south-east span-60 fragment]
<p style="line-height:50%" ><br><br><br><br>&nbsp;<br>&nbsp;</p>
@box[bg-grey-05 text-white my-box-pad2  ](<p style="line-height:40%" align="left"><span style="font-size:0.650em; " >&nbsp;&nbsp;MinnowBoard Max Silicon</span><br><span style="font-size:0.450em; font-family:Consolas; " >&nbsp;&nbsp;&lt;Memory Cntrl North&gt; <br>&nbsp;&nbsp;&nbsp;&nbsp;Vlv2DeviceRefCodePkg/ValleyView2Soc/NorthCluster<br>&nbsp;&nbsp;&lt;I/O Cntrl South &gt; <br>&nbsp;&nbsp;&nbsp;&nbsp;Vlv2DeviceRefCodePkg/ValleyView2Soc/SouthCluster<br>&nbsp;&nbsp;&nbsp;&nbsp;</span></p>)
@snapend





Note:

-  MinnowBoard Max
  -  <Memory Cntrl> Vlv2DeviceRefCodePkg/ValleyView2Soc/NorthCluster
  -  <PchX South> Vlv2DeviceRefCodePkg/ValleyView2Soc/SouthCluster


---
@title[MinnowBoard Max SoC Specific Modules ]
<p align="right"><span class="gold" ><b>MinnowBoard Max SoC Specific Modules</b></span></p>

@snap[north span-30 ]
<p style="line-height:50%" ><br>&nbsp;&nbsp;</p>
@box[bg-black text-white rounded my-box-pad2  ](<p style="line-height:40%"><span style="font-size:0.7em; " >@color[yellow](CPU)<br><br><br><br><br><br><br><br><br><br><br>&nbsp;&nbsp;&nbsp;&nbsp;</span></p>)
@snapend


@snap[north-east span-30 ]
<p style="line-height:50%" ><br>&nbsp;&nbsp;</p>
@box[bg-black text-white rounded my-box-pad2  ](<p style="line-height:40%"><span style="font-size:0.7em; " >@color[yellow](North Cluster)<br><br><br><br><br><br><br><br><br><br><br>&nbsp;&nbsp;&nbsp;&nbsp;</span></p>)
@snapend


@snap[north-east span-70 ]
<br><br><br><br><br>
<p style="line-height:50%" ><br><br>&nbsp;<br>&nbsp;</p>
@box[bg-black text-white rounded my-box-pad2  ](<p style="line-height:40%"><span style="font-size:0.7em; " >@color[yellow](South Cluster)<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>&nbsp;&nbsp;&nbsp;&nbsp;</span></p>)
@snapend

@snap[north-west span-35 ]
<p style="line-height:50%" ><br>&nbsp;&nbsp;</p>
<p style="line-height:60%" align="left"><span style="font-size:0.6em; " >
`Vlv2DeviceRefCodePkg`/<br>
&nbsp;&nbsp;&nbsp;&nbsp;`ValleyView2Soc`/ <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;CPU /<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`NorthCluster` /<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`SouthCluster` /
</span></p>
@snapend

@snap[south-west span-35 ]
<p style="line-height:50%" align="left"><span style="font-size:0.5em; " >
@color[yellow](Other SOC )&nbsp;&nbsp;- &nbsp;&nbsp;Broxton Silicon <br>
&nbsp;&nbsp;&nbsp;&nbsp;Reference package<br>
&nbsp;`BroxtonSoc/BroxtonSiPkg`/ <br>
</span></p>
@snapend


@snap[north span-30 ]
<p style="line-height:50%" ><br>&nbsp;<br>&nbsp;</p>
<p style="line-height:40%" align="left"><span style="font-size:0.450em; font-family:Consolas; " >&nbsp;&nbsp;<br>&nbsp;&nbsp;&nbsp;&nbsp;
CpuInit&nbsp;&nbsp;<br>&nbsp;&nbsp;&nbsp;&nbsp;
CpuS3&nbsp;&nbsp;<br>&nbsp;&nbsp;&nbsp;&nbsp;
Dts&nbsp;&nbsp;<br>&nbsp;&nbsp;&nbsp;&nbsp;
EcpOnly&nbsp;&nbsp;<br>&nbsp;&nbsp;&nbsp;&nbsp;
PowerManagement<br>&nbsp;&nbsp;&nbsp;&nbsp;
SmmAccess&nbsp;&nbsp;<br>&nbsp;&nbsp;&nbsp;&nbsp;
SmmControl
</span></p>
@snapend

@snap[north-east span-30 ]
<p style="line-height:50%" ><br>&nbsp;<br>&nbsp;</p>
<p style="line-height:40%" align="left"><span style="font-size:0.450em; font-family:Consolas; " >&nbsp;&nbsp;<br>&nbsp;&nbsp;
ISPDxe&nbsp;&nbsp;<br>&nbsp;&nbsp;
MemoryInit&nbsp;&nbsp;<br>&nbsp;&nbsp;
PciHostBridge&nbsp;&nbsp;<br>&nbsp;&nbsp;
SmBiosMemory&nbsp;&nbsp;<br>&nbsp;&nbsp;
VlvInit
</span></p>
@snapend

@snap[north-east span-65 ]
<br><br><br><br><br><br>
<p style="line-height:50%" ><br><br>&nbsp;<br>&nbsp;</p>
<p style="line-height:40%" align="left"><span style="font-size:0.450em; font-family:Consolas; " ><br>&nbsp;&nbsp;
PchInit&nbsp;&nbsp;<br>&nbsp;&nbsp;
Smbus&nbsp;&nbsp;<br>&nbsp;&nbsp;
Spi&nbsp;&nbsp;<br>&nbsp;&nbsp;
SmmControl&nbsp;&nbsp;<br>&nbsp;&nbsp;
Usb&nbsp;&nbsp;<br>&nbsp;&nbsp;
S3Support&nbsp;&nbsp;<br>&nbsp;&nbsp;
SmartTimer&nbsp;&nbsp;<br>&nbsp;&nbsp;
LegacyInterrupt&nbsp;&nbsp;<br>&nbsp;&nbsp;
ActiveBios&nbsp;&nbsp;<br>&nbsp;&nbsp;
</span></p>
@snapend

@snap[north-east span-35 ]
<br><br><br><br><br><br>
<p style="line-height:50%" ><br><br>&nbsp;<br>&nbsp;</p>
<p style="line-height:40%" align="left"><span style="font-size:0.450em; font-family:Consolas; " ><br>&nbsp;&nbsp;
Reset<br>&nbsp;&nbsp;
PchSmiDispatcher<br>&nbsp;&nbsp;
Pcie&nbsp;&nbsp;<br>&nbsp;&nbsp;
Pnp&nbsp;&nbsp;<br>&nbsp;&nbsp;
SDControllerDxe<br>&nbsp;&nbsp;
SDMediaDeviceDxe<br>&nbsp;&nbsp;
SataControler<br>&nbsp;&nbsp;
SysFwUpdateCapsule<br>&nbsp;&nbsp;
I2cStack
</span></p>
@snapend

Note:
-  Vlv2DeviceRefCodePkg/
  -  ValleyView2Soc/ 
    -  CPU
    -  NorthCluster
    -  SouthCluster

-  Other SOC 
	  -  Broxton Silicon Ref package
	  -  BroxtonSoc/BroxtonSiPkg/ 



---?image=/assets/images/slides/Slide28_1.JPG
@title[DXE Base Address, PCD Example ]
<!---  PCD Example   -->
<p align="right"><span class="gold" ><b>DXE Base Address, PCD Example</b></span></p>


@snap[north-east span-90 fragment]
<p align="left" style="line-height:40%"><span style="font-size:0.8em; ">
<br>
<br>
<br>
Defined in Package `MdePkg` DEC </span></p>
@box[bg-black text-white my-box-pad2  ](<p style="line-height:40%" align="left"><span style="font-size:0.450em; font-family:Consolas; " >&nbsp;&nbsp;[PcdsFixedAtBuildPcds, PatchableInModule, PcdsDynamic, PcdsDynamicEx]<br>&nbsp;&nbsp;gEfiMdePkgTokenSpaceGuid.@color[red](PcdPciExpressBaseAddress)|0|UINT64|0x0000000a&nbsp;&nbsp;</span></p>)
@snapend

@snap[north-east span-90 fragment]
<br>
<p align="left" style="line-height:40%"><span style="font-size:0.8em; ">
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
Module INF lists which PCDs get accessed</span></p>
@box[bg-black text-white my-box-pad2  ](<p style="line-height:40%" align="left"><span style="font-size:0.450em; font-family:Consolas; " >&nbsp;&nbsp;&lt;Pchx&gt;Pkg/Library/DxeRuntimePciLibPciExpress.inf<br>&nbsp;&nbsp;[Pcd]<br>&nbsp;&nbsp;gEfiMdeTokenSpaceGuid.@color[red](PcdPciExpressBaseAddress) <br>&nbsp;&nbsp;</span></p>)
@snapend


@snap[north-east span-90 fragment]
<br>
<br>
<br>
<p align="left" style="line-height:40%"><span style="font-size:0.8em; "><br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>Value to use in Project @color[yellow](`NewProjectPkg.dsc`) </span></p>
@box[bg-black text-white my-box-pad2  ](<p style="line-height:40%" align="left"><span style="font-size:0.450em; font-family:Consolas; " >&nbsp;&nbsp;[PcdsPatchableInModule]<br>&nbsp;&nbsp;gEifMdeTokenSpaceGuid.@color[red](PcdPciExpressBaseAddres)|<font color="cyan">0xE0000000</font><br>&nbsp;&nbsp;</span></p>)
@snapend


@snap[north-east span-90 fragment]
<br>
<br>
<br>
<br>
<p align="left" style="line-height:40%"><span style="font-size:0.8em; "><br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
DXE - Referenced in the DXE code in </span></p>
@box[bg-black text-white my-box-pad2  ](<p style="line-height:40%" align="left"><span style="font-size:0.450em; font-family:Consolas; " >&nbsp;&nbsp;&lt;PchX&gt;Pkg/Library/DxeRuntimePciLibPciExpress.c &nbsp;&nbsp;&nbsp;&nbsp;<br>&nbsp;&nbsp; &nbsp;&nbsp;mPciExpressBaseAddress = &lpar;UINTN&rpar; PatchPcdGet64 <br>&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp; &lpar;@color[red](PcdPciExpressBaseAddress)&rpar;;<br>&nbsp;&nbsp;&nbsp;&nbsp;</span></p>)
<br>
@snapend






Note:
-  Example of a PCD during DXE

-  Defined in ICH X Package DEC
	-  [PcdsDynamic.common]
     -  	gEfiIchTokenSpaceGuid.PcdIchSataPataConfigs|0|UINT8|0x40000016
-  The Module INF lists which PCDs get accessed
	  -  [Pcd]
	    -  gEfiIchTokenSpaceGuid.PcdIchSataPataConfigs
-  The Value to use in New Project Package DSC
	  -  [PcdsDynamicDefault.common.DEFAULT]
	    -  gEfiIchTokenSpaceGuid.PcdIchSataPataConfigs|0

-  Here is an example used in the CODE
-  DXE - Referenced in the DXE code in NewProjectPkg/ SetupDxe/Platform.c
	 
  -  	IchSataPataConfigs.Uint8 = PcdGet8(PcdIchSataPataConfigs);
  -  	PcdSet8(PcdIchSataPataConfigs, IchSataPataConfigs.Uint8);


---?image=/assets/images/slides/Slide53_1.JPG
@title[BDS Phase:]
<p align="center"><span class="gold" ><b>BDS Phase:</b></span></p>
 
<div class="left-2">
<span style="font-size:0.8em" > &nbsp;</span>
</div>
<div class="right-2">
<br>
<br>
<ul style="list-style-type:none">
  <li><span style="font-size:0.9em" ><font color="white">Detect console devices (input and output) </font> </span></li><br>
  <li><span style="font-size:0.9em" ><font color="cyan">Check enumeration of all devices preset </font> </span></li><br>
  <li><span style="font-size:0.9em" ><font color="white">Detect boot policy</font> </span></li><br>
  <li><span style="font-size:0.9em" ><font color="cyan">Ensure BIOS “front page” is loaded </font> </span></li>

  </ul>
</div>		

Note:
 
-  Detect console devices (input and output)

-  Check enumeration of all devices preset
-  another Note; BIOS must have device drivers to enumerate

-  Detection of boot policy

-  Loading of BIOS “front page”
-  Splash screen logo, messages to user, etc.


---?image=/assets/images/slides/Slide128.JPG
@title[BDS Phase - stack]
<p align="right"><span class="gold" ><b>BDS Phase</b></span></p>
 
Note:

-  Here is a picture of the protocol stack for the serial terminal console services. This details the protocols that are necessary for getting output on the serial terminal.

-  UEFI and the framework do not directly hard code input/output or console devices to another driver or program. They instead rely upon console devices to produce a Simple Text Input and Simple Text Output protocol. They consume from those protocols. Thus you can write your application free of worry where input and output will be going. 

-  To allow many devices to produce input and output, there is a virtual console or console splitter that gathers input from different devices and sends output to different devices. Thus the BDS or UEFI Shell is not directly connected to VGA or serial port. It sends output to the virtual console which in turns send that output to any device that is connected to it that has published the Simple Text Output Protocol.

-  In the porting aspect, once ISA I/O protocol driver is ported and the underlying protocols it depends on, the Serial I/O driver can be ported and then the BDS and/or UEFI shell can be used as-is to continue with your porting and debugging effort.



---?image=/assets/images/slides/Slide130.JPG
@title[Serial Terminal Console Drivers]
<p align="right"><span class="gold" ><b>Serial Terminal Console Drivers</b></span></p>
 
Note:

-  Here is a table of the drivers used. The drivers in green do not require any changes for your platform. You may have changes in your ISA serial if the UARTs are different than the normal PCAT UARTs

-  The Console splitter may require changes if your default serial port is not the same as the default one – baud rate, COM port, etc.

-  The orange ones (or chipset specific) are the base protocols that need platform porting if yours is different than our reference implementation
 
 

---?
@title[Porting Serial Terminal Console]
<p align="right"><span class="gold" ><b>Porting Serial Terminal Console</b></span></p>

@snap[north-west span-90 ]
<br>
<br>
<p align="left" style="line-height:40%"><span style="font-size:0.8em; "><br></span></p>
@box[bg-black text-yellow rounded my-box-pad2  ](<p style="line-height:40%" align="left"><span style="font-size:0.50em; font-family:Consolas; " >&nbsp;&nbsp;@color[white](NewProjectPkg/)<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;PlatformDxe/<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;   PlatformSetupDxe /<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;	@color[red](. . .)<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;   Library/<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;      PlatformBdsLib/<br>&nbsp;&nbsp;&nbsp;&nbsp;</span></p>)
<br>
@snapend


@snap[north-west span-90 ]
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<p align="left" style="line-height:40%"><span style="font-size:0.8em; "><br></span></p>
@box[bg-black text-white rounded my-box-pad2  ](<p style="line-height:40%" align="left"><span style="font-size:0.50em; font-family:Consolas; " ><font color="cyan">&nbsp;&nbsp;@color[white](MdeModulePkg/)<br>&nbsp;&nbsp;&nbsp;&nbsp; Universal/<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  Console/<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ConPlatformDxe/<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  ConSplitterDxe/<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  GraphicsConsoleDxe/<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  TerminalDxe/<br>&nbsp;&nbsp;&nbsp;&nbsp;</font></span></p>)
<br>
@snapend



@snap[north-east span-30 fragment ]
<br>
<br>
<br>
<p align="left" style="line-height:40%"><span style="font-size:0.8em; "><br></span></p>
![Platform](/assets/images/platform.png)
<br>
<br>
<br>
![OpenSource](/assets/images/OpenSource.png)
@snapend

 
Note:
-  Example platform
-  specific location
  -  EDK II Open
  -  Source location




---?image=assets/images/binary-strings-black2.jpg
<!-- .slide: data-transition="none" -->
@title[Porting Task List Section 05]
<p align="center"><span style="font-size:01.25em"><font color="#e49436"><b>Porting Task List</b></span></p>

@snap[north-east span-90 ]
<br>
<br>
<br>
@box[bg-grey-15 text-white rounded my-box-pad2  ](<p style="line-height:60%" ><span style="font-size:0.9em; font-weight: bold;" > <br><br> <br><br><br><br><br><br><br><br><br><br><br><br><br>&nbsp;</span></p>)
@snapend


@snap[north-east span-15]
![Porting_task_list.gif](/assets/images/tenor.gif)
@snapend

<!---  col of numbers  -->

@snap[north-west span-10 ]
<br>
<br>
<p style="line-height:60%" align="left"><span style="font-size:02.0em" ><font color="#808080"><br>@color[yellow](&#10102;<br><br>&#10103;<br><br>&#10104;<br><br>&#10105;)<br><br>@color[red](&#10106;)<br><br>@color[#808080](&#10107;)  </font></span></p>
@snapend


@snap[north-east span-90 ]
<br>
<br>
<p style="line-height:60%" align="left"><span style="font-size:0.85em" ><br>&nbsp;@color[gray](Create a New Project package directory)
<br><br><br>&nbsp;@color[gray](Create Build Files &lpar;DSC, DEC, and FDF&rpar;)
<br><br><br>&nbsp;@color[gray](Update target.txt to make your Project the default)
<br><br><br>&nbsp;@color[gray](Use UEFI PI phases to Port all project modules)
<br><br><br>&nbsp;@color[yellow](Update DSC w/ new libraries, modules, and PCDs values)
<br><br><br>&nbsp;@color[gray](Minimums for UEFI Shell)</font></span></p>
@snapend


@snap[south span-100 fragment]
@box[bg-purple-pp text-white rounded my-box-pad2  ](<p style="line-height:80%"><span style="font-size:0.80em" >Update build text files with libraries, ported modules, and PCD values to configure modules<br>&nbsp;</span></p>)
@snapend
Note:

1. Create a New Project package directory
2. Create Build Files (DSC, DEC, and FDF)
3. Update conf/target.txt to make your Project the default build (optional)  
4. Port all required modules for your project through all UEFI Platform initialization phases
5. Update build text (DSC, DEC, FDF) files with libraries, ported modules, and PCD values to configure modules
6. Minimums for UEFI Shell


### Section 5 of the Porting Task List
 -  Update build text files with libraries, ported modules, and PCD values to configure modules



---
@title[Build Text Files for the Platform]
<p align="right"><span class="gold" ><b>Build Text Files for the Platform</b></span></p>

@snap[north span-50]
<br>
<p align="left" style="line-height:40%"><span style="font-size:0.8em; "><br><br></span></p>
@box[bg-black text-white rounded my-box-pad2  ](<p style="line-height:80%" align="left"><span style="font-size:0.70em; font-family:Consolas; " >&nbsp;&nbsp;MyWorkSpace/<br>&nbsp;&nbsp;&nbsp;&nbsp;	NewProjectPkg/<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;		Include/<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;		Library/<br>&nbsp;&nbsp;<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;		PlatformDrivers/<br>&nbsp;&nbsp;	<br>	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;		NewProjectPkg.DSC<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;		NewProjectPkg.FDF<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;		NewProjectPkg.DEC<br>&nbsp;&nbsp;&nbsp;&nbsp;</span></p>)
<br>
@snapend


@snap[west span-40 fragment]
<br>
<br>
<br>
<br>
<p align="left" style="line-height:40%"><span style="font-size:0.8em; "><br><br></span></p>
<p align="right" style="line-height:80%"><span style="font-size:0.7em; "><br>@color[yellow](<b>Flash Map Layout</b>&nbsp;&nbsp;&rarr;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;)</span></p>
@snapend

@snap[east span-40 fragment]
<br>
<br>
<br>
<p align="left" style="line-height:40%"><span style="font-size:0.8em; "><br><br><br><br></span></p>
<p align="left" style="line-height:60%"><span style="font-size:0.7em; ">@color[yellow](&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&larr;&nbsp;&nbsp;<b>PCD Values - Library)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; @color[yellow](classes</b>)</span></p>
@snapend


@snap[south-east span-40 fragment]
<p align="left" style="line-height:80%"><span style="font-size:0.7em; ">@color[yellow](&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&larr;&nbsp;&nbsp;<b>Defines for a platform</b>)</span></p>
<p align="left" style="line-height:40%"><span style="font-size:0.8em; "><br></span></p>
<br>
<br>
@snapend


@snap[south-west span-60 ]
<span style="font-size:0.5em" >Check the <a href="https://github.com/tianocore/tianocore.github.io/wiki/EDK-II-Specifications">EDK II Specifications</a> </span>
@snapend


Note:
-  Specs:
  -  https://github.com/tianocore/tianocore.github.io/wiki/EDK-II-Specifications

- PCD Values - Library classes -	NewProjectPkg.DSC
- Flash Map layout 	-	NewProjectPkg.FDF
- Defines for a platform -	NewProjectPkg.DEC



---?image=/assets/images/slides/Slide139.JPG
@title[Update the New Project DEC File]
<p align="right"><span class="gold" ><b>Update the New Project DEC File</b></span></p>
<br> 
<br> 
<br> 
<br> 
<br> 
<br> 
<br> 
<br> 
<br>
<span style="font-size:0.5em" > Example DEC file for NewProjectPkg - Next slide</span>

Note:


-  Update the PCD used by the New Project Package 
-  Update for the Libraries and Protocols used by the New Project Package
-  See EDK II DEC File Specification for more details and examples 



+++?code=sample/NewProjectPORT/NewProjectPkg.dec&lang=shell&title=Example: DEC file


Note:
 This is an example of the NewProjectPkg.dec file
 Look at the GUID, Protocol and PCD declarations


---?image=/assets/images/slides/Slide141.JPG
@title[Update the New Project DSC File]
<p align="right"><span class="gold" ><b>Update the New Project DSC File</b></span></p>
<br> 
<br> 
<br> 
<br> 
<br> 
<br> 
<br> 
<br> 
<br> 
<span style="font-size:0.5em" > Example DSC file for NewProjectPkg - Next slide</span>

Note:

-  Update to define all libraries, components and/or modules that will be used by the New Project package
-  Update the PCD Values for the New Project 
-  Update any library classes
-  See EDK II DSC File Specification for more details and examples 


+++?code=sample/NewProjectPORT/NewProjectPkg.dsc&lang=shell&title=Example: DSC file


Note:
 This is an example of the NewProjectPkg.dsc file



---?image=/assets/images/slides/Slide143.JPG
<!-- .slide: data-transition="none" -->
@title[Update the New Project FDF File]
<p align="right"><span class="gold" ><b>Update the New Project FDF File</b></span></p>
<br> 
<br> 
<br> 
<br> 
<br> 
<br> 
<br> 
<br> 
<br>
<span style="font-size:0.5em" > Example FDF file for NewProjectPkg - Next slides</span>

Note:
-  Rules for combining binaries (Firmware Image) built from a DSC file
-  PCDs set in the FDF file for Addresses, Sizes, and other "fixed" information needed to define or create the flash image 
-  See EDK II FDF File Specification for more details and examples 

-  Used to define what components or modules are placed within a flash device (FD) file
-  Defines order the components and modules are positioned within the image
-  Consists of define statements, set statements and module statements (INF files to be used)


+++?image=/assets/images/slides/Slide145.JPG
<!-- .slide: data-background-transition="none" -->
<!-- .slide: data-transition="none" -->
@title[Update the New Project FDF File Layout]
<p align="right"><span class="gold" ><b>Update the New Project FDF File - Layout</b></span></p>



Note:
Flash Device Configuration Common Layout File (.fdf)


+++?code=sample/NewProjectPORT/NewProjectPkg.fdf&lang=shell&title=Example: FDF file


Note:
 This is an example of the NewProjectPkg.fdf file

 
+++
@title[FDF File Example]
<p align="right"><span class="gold" >FDF File Example</span></p>


```C
[Fv.Root]
FvAlignment = 64
ERASE_POLARITY = 1
MEMORY_MAPPED = TRUE
STICKY_WRITE = TRUE
. . .
INF VERSION = "1" $(WS)/EdkNt32Pkg/ Dxe/WinNtThunk/Cpu/Cpu.inf
FILE DXE_CORE = B5596C75-37A2-4. . .{
  SECTION COMPRESS { . . .}


DEFINE DC = $(WS)/Build/NewProjectPkg 	/DEBUG_MYTOOLS
    SECTION PE32 = $(DC)/B5596C75-3 . . .     	-DxeCore.efi
    SECTION VERSION "1.2.3"
   }
}
FILE FV_IMAGE = EF41A0E1-40B1-481 . . .{
  FvAlignment = 512K
  WRITE_POLICY_RELIABLE = TRUE
  SECTION GUIDED 3EA022A4-1439-4 . . . {
    SECTION FV_IMAGE = Dxe {
    APRIORI DXE {
        INF NewProject/a/a.inf
        INF MdePkg/x/y/z.inf
        INF NewProject/a/b/b.inf
    }
      INF a/d/d.inf
      . . . 
    }
  }
DEFINE SAMPLE = MdeModulePkg/Sample 
INF $(SAMPLE)/Universal/Network/ Ip4Dxe/Ip4Dxe.inf
INF $(SAMPLE)/Universal/Network/ Ip4ConfigDxe/Ip4ConfigDxe.inf 
INF $(SAMPLE)/Universal/Network/ Udp4Dxe/Udp4Dxe.inf 
INF $(SAMPLE)/Universal/Network/ Tcp4Dxe/Tcp4Dxe.inf 
INF $(SAMPLE)/Universal/Network/ Dhcp4Dxe/Dhcp4Dxe.inf 
INF $(SAMPLE)/Universal/Network/ Mtftp4Dxe/Mtftp4Dxe.inf 
INF $(SAMPLE)/Universal/Network/ SnpNt32Dxe/SnpNt32Dxe.inf 

```






---?image=assets/images/binary-strings-black2.jpg
@title[Porting Task List Section 06]
<p align="center"><span style="font-size:01.25em"><font color="#e49436"><b>Porting Task List</b></span></p>

@snap[north-east span-90 ]
<br>
<br>
<br>
@box[bg-grey-15 text-white rounded my-box-pad2  ](<p style="line-height:60%" ><span style="font-size:0.9em; font-weight: bold;" > <br><br> <br><br><br><br><br><br><br><br><br><br><br><br><br>&nbsp;</span></p>)
@snapend


@snap[north-east span-15]
![Porting_task_list.gif](/assets/images/tenor.gif)
@snapend

<!---  col of numbers  -->

@snap[north-west span-10 ]
<br>
<br>
<p style="line-height:60%" align="left"><span style="font-size:02.0em" ><font color="#808080"><br>@color[yellow](&#10102;<br><br>&#10103;<br><br>&#10104;<br><br>&#10105;<br><br>&#10106;)<br><br>@color[red](&#10107;)  </font></span></p>
@snapend


@snap[north-east span-90 ]
<br>
<br>
<p style="line-height:60%" align="left"><span style="font-size:0.85em" ><br>&nbsp;@color[gray](Create a New Project package directory)
<br><br><br>&nbsp;@color[gray](Create Build Files &lpar;DSC, DEC, and FDF&rpar;)
<br><br><br>&nbsp;@color[gray](Update target.txt to make your Project the default)
<br><br><br>&nbsp;@color[gray](Use UEFI PI phases to Port all project modules)
<br><br><br>&nbsp;@color[gray](Update DSC w/ new libraries, modules, and PCDs values)
<br><br><br>&nbsp;@color[yellow](Minimums for UEFI Shell)</font></span></p>
@snapend


@snap[south span-100 fragment]
@box[bg-purple-pp text-white rounded my-box-pad2  ](<p style="line-height:80%"><span style="font-size:0.80em" >Double check the Protocol, Driver dependencies and libraries<br> to boot to the UEFI Shell<br>&nbsp;</span></p>)
@snapend

Note:

1. Create a New Project package directory
2. Create Build Files (DSC, DEC, and FDF)
3. Update conf/target.txt to make your Project the default build (optional)  
4. Port all required modules for your project through all UEFI Platform initialization phases
5. Update build text (DSC, DEC, FDF) files with libraries, ported modules, and PCD values to configure modules
6. Minimums for UEFI Shell

### Section 6 of the Porting Task List
 -  Minimums for UEFI Shell



---?image=/assets/images/slides/Slide150.JPG
@title[Minimum Drivers for UEFI Shell]
<p align="right"><span class="gold" ><b>Minimum Drivers for UEFI Shell</b></span></p>

Note:
Here we have a summary of the drivers that will most likely need changing for your port to a new platform to bring up the EFI shell. As you can see the list is not that long. If your platform is similar to one of our reference platforms (same chipset typically) then your porting effort will mostly be in the area of MRC, Super I/O and PCI infrastructure (servers may have multiple root bus bridges)

The goodness about this is that you can bring the shell up and then via serial port interact with the shell to load and test new drivers as well as your port to this point.

-  MinnowBoard Max
  -  <Memory Cntrl North> Vlv2DeviceRefCodePkg/ValleyView2Soc/NorthCluster
  -  <I/O Cntrl South> Vlv2DeviceRefCodePkg/ValleyView2Soc/SouthCluster




---?image=/assets/images/slides/Slide152.JPG
@title[Minimum Libraries for UEFI Shell]
<p align="right"><span class="gold" ><b>Minimum Libraries for UEFI Shell</b></span></p>

Note:
Just be aware of Shell libraries that would be interfacing with the platform for porting

-  MinnowBoard Max
  -  <I/O Cntrl South> Vlv2DeviceRefCodePkg/ValleyView2Soc/SouthCluster

---?
@title[Porting Summary: New Package Directory]
<p align="right"><span class="gold" ><b>Porting Summary: New Package Directory</b></span></p>

@snap[north-west span-50]
<br>
<p align="left" style="line-height:40%"><span style="font-size:0.8em; "><br><br></span></p>
@box[bg-black text-white rounded my-box-pad2  ](<p style="line-height:80%" align="left"><span style="font-size:0.70em; font-family:Consolas; " >&nbsp;&nbsp;MyWorkSpace/<br>&nbsp;&nbsp;&nbsp;&nbsp;	NewProjectPkg/<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;		Include/<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;		Library/<br>&nbsp;&nbsp;<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;		PlatformDrivers/<br><br>&nbsp;&nbsp;	<br>	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;		NewProjectPkg.DSC<br><br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;		NewProjectPkg.FDF<br><br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;		NewProjectPkg.DEC<br>&nbsp;&nbsp;&nbsp;&nbsp;</span></p>)
<br>
@snapend


@snap[north-east span-40]
<br>
<p align="left" style="line-height:40%"><span style="font-size:0.8em; "><br></span></p>
<p style="line-height:80%" align="left"><span style="font-size:01.20em;" >Ported Package</span></p>
<br>
@snapend


@snap[north-east span-50 fragment]
<br>
<p align="left" style="line-height:40%"><span style="font-size:0.8em; "><br></span></p>
<p style="line-height:70%" align="left"><span style="font-size:0.80em; " ><font color="yellow">
<br><br><br>
<br>&nbsp;&nbsp;&nbsp;&nbsp;
@size[1.52em](@fa[star gp-bullet-ltgreen])&nbsp;&nbsp;All ported libraries
</font></span></p>
<br>
@snapend


@snap[north-east span-50 fragment]
<br>
<p align="left" style="line-height:40%"><span style="font-size:0.8em; "><br><br></span></p>
<p style="line-height:70%" align="left"><span style="font-size:0.80em; " ><font color="yellow">
<br><br><br>
<br>&nbsp;&nbsp;&nbsp;&nbsp;
<br><br>&nbsp;&nbsp;&nbsp;&nbsp;
@size[1.52em](@fa[star gp-bullet-gold])&nbsp;&nbsp;All ported Drivers
</font></span></p>
<br>
@snapend


@snap[north-east span-50 fragment]
<br>
<p align="left" style="line-height:40%"><span style="font-size:0.8em; "><br></span></p>
<p style="line-height:70%" align="left"><span style="font-size:0.80em; " ><font color="yellow">
<br><br><br><br>
<br>&nbsp;&nbsp;&nbsp;&nbsp;
<br><br>&nbsp;&nbsp;&nbsp;&nbsp;
<br><br><br>&nbsp;&nbsp;&nbsp;&nbsp;
@size[1.52em](@fa[star gp-bullet-magenta])&nbsp;&nbsp;Values – Library classes
</font></span></p>
<br>
@snapend


@snap[north-east span-50 fragment]
<br>
<p align="left" style="line-height:40%"><span style="font-size:0.8em; "><br></span></p>
<p style="line-height:70%" align="left"><span style="font-size:0.80em; " ><font color="yellow">
<br><br><br><br>
<br>&nbsp;&nbsp;&nbsp;&nbsp;
<br><br>&nbsp;&nbsp;&nbsp;&nbsp;
<br><br><br>&nbsp;&nbsp;&nbsp;&nbsp;
<br><br>&nbsp;&nbsp;&nbsp;&nbsp;
@size[1.52em](@fa[star gp-bullet-cyan])&nbsp;&nbsp;Flash Map layout
</font></span></p>
<br>
@snapend


@snap[north-east span-50 fragment]
<br>
<p align="left" style="line-height:40%"><span style="font-size:0.8em; "><br><br></span></p>
<p style="line-height:70%" align="left"><span style="font-size:0.80em; " ><font color="yellow">
<br><br><br><br>
<br>&nbsp;&nbsp;&nbsp;&nbsp;
<br><br>&nbsp;&nbsp;&nbsp;&nbsp;
<br><br><br>&nbsp;&nbsp;&nbsp;&nbsp;
<br><br>&nbsp;&nbsp;&nbsp;&nbsp;
<br><br>&nbsp;&nbsp;&nbsp;&nbsp;
@size[1.52em](@fa[star gp-bullet-blue])&nbsp;&nbsp;Defines per platform
</font></span></p>
<br>
@snapend


Note:




  
---  
@title[Summary]
<BR>
### <p align="center"><span class="gold"   >Summary </span></p><br>
<ul style="list-style-type:none">
 <li>@fa[certificate gp-bullet-green]<span style="font-size:0.9em">&nbsp;&nbsp;Define the porting task list for porting existing<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; platforms in EDK II in order to boot to the UEFI Shell</span> </li>
 <li>@fa[certificate gp-bullet-cyan]<span style="font-size:0.9em">&nbsp;&nbsp;Explain the EDK II infrastructure, porting libraries,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; library classes, PCDs, and directory structures</span></li>
 <li>@fa[certificate gp-bullet-yellow]<span style="font-size:0.9em">&nbsp;&nbsp;Determine the necessary porting for each phase<br> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;of a new EDK II platform Project</span> </li>
</ul>


---?image=assets/images/gitpitch-audience.jpg
@title[Questions]
<br>
![Questions](/assets/images/questions.JPG) 


---?image=assets/images/gitpitch-audience.jpg
@title[Logo Slide]
<br><br><br>
![Logo Slide](/assets/images/TianocoreLogo.png =10x)


---
@title[Acknowledgements]
#### <p align="center"><span class="gold"   >Acknowledgements</span></p>

```c++
/**
Redistribution and use in source (original document form) and 'compiled' forms (converted
to PDF, epub, HTML and other formats) with or without modification, are permitted provided
that the following conditions are met:

Redistributions of source code (original document form) must retain the above copyright 
notice, this list of conditions and the following disclaimer as the first lines of this 
file unmodified.

Redistributions in compiled form (transformed to other DTDs, converted to PDF, epub, HTML
and other formats) must reproduce the above copyright notice, this list of conditions and 
the following disclaimer in the documentation and/or other materials provided with the 
distribution.

THIS DOCUMENTATION IS PROVIDED BY TIANOCORE PROJECT "AS IS" AND ANY EXPRESS OR IMPLIED 
WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND 
FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL TIANOCORE PROJECT BE 
LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES 
(INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, 
DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, 
WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) 
ARISING IN ANY WAY OUT OF THE USE OF THIS DOCUMENTATION, EVEN IF ADVISED OF THE POSSIBILITY 
OF SUCH DAMAGE.

Copyright (c) 2018, Intel Corporation. All rights reserved.
**/

```
