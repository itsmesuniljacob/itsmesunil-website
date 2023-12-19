---
title: "Do you tolerate duplicate code\_?"
description: >-
  One of the stems in achieving code quality is to avoid duplication in the
  source code. There are no best practices in this area and some…
date: '2019-01-15T14:35:41.786Z'
categories: ["practice"]
keywords: []
slug: /@itsmesunil/do-you-tolerate-duplicate-code
draft: false
---

![](/img/0__P3y4__Tm4Sl5dxdfi.jpg)

One of the stems in achieving code quality is to avoid duplication in the source code. There are no best practices in this area and some practices proven in some contexts, may not be good for others. Duplication in code causes the program to have more lines of unnecessary code. Bigger is not always better when it comes to software. Clean code practices do not have to be an expensive or a major undertaking. It is about being able to improve incrementally and achieve a significant cumulative impact on the improvement journey.

### What exactly is duplicate code?

> **Duplicate code** is a computer programming term for a sequence of source code that occurs more than once, either within a program or across different programs owned or maintained by the same entity.

Source: [wiki](https://en.wikipedia.org/wiki/Duplicate_code)

Duplication usually occurs when multiple programmers are working on the same file or by the usual practice of copy/paste. Duplicate code can be created, when using a section of copied code. Usually, this type of code is used with slight modifications, such as renaming variables, changing values of constants or adding/deleting code. Under time constraints many developers do the same and term as re-use technique. Usually in real-world duplication is considered to be a major problem when it gets out of control.

> “The way you get programmer productivity is by eliminating lines of code you have to write” — Steve Jobs

**What are the problems with code duplication?**

In long-term, the implications of code duplication can be very negative. Common problems could be:

*   Increase in code size: It would be difficult to maintain an application which has redundant code. This will cost time and money for the organization
*   Introduce bugs: If the redundant code is there in 10 files of software and change is done only in 8 places, a bug is introduced

Practice the method of writing DRY (Don’t Repeat Yourself) which makes your code more efficient and readable.

On a lighter note duplication is not serious if your code is throwaway code, but if you expect your code to live for years it’s something that needs attention.

Below is very basic example of Power shell script, which accepts a set of default parameters and mandatory parameters ( `Workspace` and `Id )`.

#**Param.ps1**  
Param  
(  
 \[string\]$Workspace = $(Throw ‘-Workspace is required’),  
 $ComponentName = “Arduino”,  
 $CompanyName = “XYZ Software”,  
 $CopyRight = “Scorpio Technologies”,  
 $ProductName = “Micro Controller”,  
 \[string\]$Id = $(Throw ‘-Id is required’)

)

The script can be run using the below command in PowerShell editor:

`param.ps1 -Workspace 'MyPC' -Id '624'`

As most of the language has its own framework to write unit test cases, Power shell uses Pester framework for writing unit test cases. The initial Pester script for unit testing the `Param.ps1` is put on view below:

$Params = @{  
  Workspace = 'MyPC'  
  ComponentName = 'Arduino'  
  CompanyName = 'XYZ Software'  
  CopyRight = 'Scorpio Technologies'  
  ProductName = 'Micro Controller'  
  BuildId = '624'  
}

$here = Split-Path -Parent $MyInvocation.MyCommand.Path  
$sut = (Split-Path -Leaf $MyInvocation.MyCommand.Path).Replace(".Tests.", ".")  
. "$here\\$sut" [@Params](http://twitter.com/Params "Twitter profile for @Params")

Describe 'Mandatory parameters' {  
    it  'Workspace' {  
        {  
            $Params = @{  
                #Workspace = 'MyPc'  
                ComponentName = 'Arduino'  
            }  
            . "$here\\$sut" [@Params](http://twitter.com/Params "Twitter profile for @Params")  
        } | Should throw '-Workspace is required'  
    }

it  'ComponentName' {  
        {  
            $Params = @{  
                Workspace = 'MyPc'  
                #ComponentName = 'Test'  
            }  
            . "$here\\$sut" [@Params](http://twitter.com/Params "Twitter profile for @Params")  
        } | Should throw '-ComponentName is required'  
    }

it  'CompanyName' {  
        {  
            $Params = @{  
                Workspace = 'MyPc'  
                ComponentName = 'Arduino'  
            }  
            . "$here\\$sut" [@Params](http://twitter.com/Params "Twitter profile for @Params")  
        } | Should throw '-CompanyName is required'  
    }

it  'CopyRight' {  
        {  
            $Params = @{  
                Workspace = 'MyPc'  
                ComponentName = 'Arudino'  
                CompanyName = 'Test'  
                #CopyRight = 'Test'  
            }  
            . "$here\\$sut" [@Params](http://twitter.com/Params "Twitter profile for @Params")  
        } | Should throw '-CopyRight is required'  
    }

it  'ProductName' {  
        {  
            $Params = @{  
                Workspace = 'MyPc'  
                ComponentName = 'Arduino'  
                CompanyName = 'Test'  
                CopyRight = 'Test'  
                #ProductName = 'Test'  
            }  
            . "$here\\$sut" [@Params](http://twitter.com/Params "Twitter profile for @Params")  
        } | Should throw '-ProductName is required'  
    }

it  'BuildId' {  
        {  
            $Params = @{  
                Workspace = 'MyPc'  
                ComponentName = 'Arduino'  
                CompanyName = 'Test'  
                CopyRight = 'Test'  
                ProductName = 'Test'  
                #BuildId = 'test'  
            }  
            . "$here\\$sut" [@Params](http://twitter.com/Params "Twitter profile for @Params")  
        } | Should throw '-BuildId is required'  
    }

}

The system under test ($SUT) refers to a system that is being validated by the testers. What are your first impressions of the test script? Although the tests ran fine, there seemed to be a potential problem. Some of the highlights are

*   Duplication in parameter checking
*   Tight coupling with the implementation
*   Lengthy code
*   Adding more parameters would again lengthen your code

It was great to take up the challenge to refactor this unit test code because duplication can cause maintainability issues. But, what would be strategy for the code above:

*   Delegate the common behavior
*   Break down the multiple fields
*   Try to apply the concept, Replace conditionals with Polymorphism ( A concept from Martin Fowler’s book Refactoring ) for the `it` block?

After applying all the thoughts above the we were able to modify the script as below:

$Params = $cases = @{  
  Workspace = 'MyPC'  
  ComponentName = 'Arduino'  
  CompanyName = 'XYZ Software'  
  CopyRight = 'Scorpio Technologies'  
  ProductName = 'Micro Conroller'  
  Id = '624'  
}

$mandatory = @('Workspace','Id')  
$here = Split-Path -Parent $MyInvocation.MyCommand.Path  
$sut = (Split-Path -Leaf $MyInvocation.MyCommand.Path).Replace(".Tests.", ".")  
. "$here\\$sut" [@Params](http://twitter.com/Params "Twitter profile for @Params")

Describe 'Mandatory parameters' {  
  for($i=0;$i -lt $mandatory.Count;$i++) {  
    it  $mandatory\[$i\] {  
        {  
            $Params = @{  
                $ComponentName = 'Arduino'  
            }  
            . "$here\\$sut" [@Params](http://twitter.com/Params "Twitter profile for @Params")  
        } | Should throw  
    }  
  }  
}

The above refactored test script looks more concise. But, needed to have a template method pattern for invoking the system under test and separate the same from the test cases.

$buildIdentifier = @{  
    Workspace = 'MyPC';  
    ComponentName = 'Arduino';   
    CompanyName = 'XYZ Software';  
    CopyRight = 'Scorpio Technologies';   
    ProductName   = 'Micro Controller';     
    Id     = '624'  
}

function Invoke-NumberUpdate(){  
  Param($buildIdentifier)  
  $here = Split-Path -Parent $MyInvocation.PSCommandPath  
  $sut = (Split-Path -Leaf   $MyInvocation.PSCommandPath).Replace(".Tests.", ".")  
  $sut = "$here\\$sut"  
  . $sut [@buildIdentifier](http://twitter.com/buildIdentifier "Twitter profile for @buildIdentifier")  
}

Describe 'Mandatory Parameter Validation' {  
    $testCases = @()  
      ("Workspace","Build") | ForEach-Object { $testCases += @(@{mandatoryParamName = "$\_"}) }  
    It ('should fail if <mandatoryParamName> is missing') -TestCases $testCases {  
        param ($mandatoryParamName)  
        $badParams = $buildIdentifier.Clone()  
        $badParams.Remove($mandatoryParamName)  
        { Invoke-BuildNumberUpdate $badParams } | Should Throw   "-$mandatoryParamName is required"  
    }  
}

### **Conclusion**

Without question, the great part was to clench the idea of Polymorphism and work towards refactoring the script effectively. Additionally , i believe there are better mechanisms for refactoring.

Feel free to post your approach. You can find me on [Twitter](https://twitter.com/itsmesunil314)/[LinkedIn](https://www.linkedin.com/in/itsmesuniljacob/).