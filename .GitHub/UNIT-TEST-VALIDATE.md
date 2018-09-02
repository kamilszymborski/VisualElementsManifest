###### DESCRIPTION
------------
The test consists in checking various cases in which inappropriate elements, properties and values appear...
<br/>
<br/>
(generated by google translator - forgive me)

###
�

###### TEST FRAGMENT - 1 - VALID
------------
```xml
<Application>
  <VisualElements
      BackgroundColor="aqua"
      ForegroundText="dark"
      ShowNameOnSquare150x150Logo="on" />
</Application>
```

###
�

###### TEST FRAGMENT - 2 - NOT VALID
------------
```xml
<Application>
  <VisualElements
      BackgroundColor="aqua"
      ForegroundText="dark"
      ShowNameOnSquare150x150Logo="on"
      Square150x150Logo="Medium-Image.png" />
</Application>
```

###
�


###### TEST FRAGMENT - 3 - VALID
------------
```xml
<Application>
  <VisualElements
      BackgroundColor="aqua"
      ForegroundText="dark"
      ShowNameOnSquare150x150Logo="on"
      Square70x70Logo="Small-Image.png"
      Square150x150Logo="Medium-Image.jpg" />
</Application>
```

###
�


###### TEST FRAGMENT - 4 - VALID
------------
```xml
<Application>
  <VisualElements
      BackgroundColor="#aaBBcc"
      ForegroundText="dark"
      ShowNameOnSquare150x150Logo="on"
      Square70x70Logo="Small-Image.gif"
      Square150x150Logo="Medium-Image.jpeg" />
</Application>
```

###
�


###### TEST FRAGMENT - 5 - NOT VALID
------------
```xml
<Application>
  <VisualElements
      BackgroundColor="Aqua"
      ForegroundText="dark"
      ShowNameOnSquare150x150Logo="on"
      Square70x70Logo="Small-Image.gif"
      Square150x150Logo="Medium-Image.jpeg" />
</Application>
```

###
�


###### TEST FRAGMENT - 6 - NOT VALID
------------
```xml
<Application>
  <VisualElements
      BackgroundColor="aqua"
      ForegroundText="Dark"
      ShowNameOnSquare150x150Logo="on"
      Square70x70Logo="Small-Image.gif"
      Square150x150Logo="Medium-Image.jpeg" />
</Application>
```

###
�


###### TEST FRAGMENT - 7 - NOT VALID
------------
```xml
<Application>
  <VisualElements
      BackgroundColor="aqua"
      ForegroundText="dark"
      ShowNameOnSquare150x150Logo="On"
      Square70x70Logo="Small-Image.gif"
      Square150x150Logo="Medium-Image.jpg" />
</Application>
```

###
�


###### TEST FRAGMENT - 8 - NOT VALID
------------
```xml
<Application>
  <VisualElements
      BackgroundColor="aqua"
      ForegroundText="dark"
      ShowNameOnSquare150x150Logo="on"
      Square70x70Logo="Small-Image.Gif"
      Square150x150Logo="Medium-Image.jpeg" />
</Application>
```

###
�


###### TEST FRAGMENT - 9 - NOT VALID
------------
```xml
<Application>
  <VisualElements
      BackgroundColor="aqua"
      ForegroundText="dark"
      ShowNameOnSquare150x150Logo="on"
      Square70x70Logo="\Small-Image.gif"
      Square150x150Logo="Medium-Image.jpeg" />
</Application>
```

###
�


###### TEST FRAGMENT - 10 - VALID
------------
```xml
<Application>
  <VisualElements
      BackgroundColor="aqua"
      ForegroundText="dark"
      ShowNameOnSquare150x150Logo="on"
      Square70x70Logo="Images\Small-Image.gif"
      Square150x150Logo="Medium-Image.jpeg" />
</Application>
```

###
�


###### TEST FRAGMENT - 11 - VALID
------------
```xml
<Application>
  <VisualElements
      BackgroundColor="aqua"
      ForegroundText="dark"
      ShowNameOnSquare150x150Logo="on"
      Square70x70Logo="C:\Images\Small-Image.gif"
      Square150x150Logo="Medium-Image.jpeg" />
</Application>
```

###
�

###### CODE
------------
```csharp
var TestFragments = new Dictionary<string, bool>
{
    {"<Application>  <VisualElements      BackgroundColor=\"aqua\"      ForegroundText=\"dark\"      ShowNameOnSquare150x150Logo=\"on\" /></Application>", true },
    {"<Application>  <VisualElements      BackgroundColor=\"aqua\"      ForegroundText=\"dark\"      ShowNameOnSquare150x150Logo=\"on\"      Square150x150Logo=\"Medium-Image.png\" /></Application>", false },
    {"<Application>  <VisualElements      BackgroundColor=\"aqua\"      ForegroundText=\"dark\"      ShowNameOnSquare150x150Logo=\"on\"      Square70x70Logo=\"Small-Image.png\"      Square150x150Logo=\"Medium-Image.jpg\" /></Application>", true },
    {"<Application>  <VisualElements      BackgroundColor=\"#aaBBcc\"      ForegroundText=\"dark\"      ShowNameOnSquare150x150Logo=\"on\"      Square70x70Logo=\"Small-Image.gif\"      Square150x150Logo=\"Medium-Image.jpeg\" /></Application>", true },
    {"<Application>  <VisualElements      BackgroundColor=\"Aqua\"      ForegroundText=\"dark\"      ShowNameOnSquare150x150Logo=\"on\"      Square70x70Logo=\"Small-Image.gif\"      Square150x150Logo=\"Medium-Image.jpeg\" /></Application>", false },
    {"<Application>  <VisualElements      BackgroundColor=\"aqua\"      ForegroundText=\"Dark\"      ShowNameOnSquare150x150Logo=\"on\"      Square70x70Logo=\"Small-Image.gif\"      Square150x150Logo=\"Medium-Image.jpeg\" /></Application>", false },
    {"<Application>  <VisualElements      BackgroundColor=\"aqua\"      ForegroundText=\"dark\"      ShowNameOnSquare150x150Logo=\"On\"      Square70x70Logo=\"Small-Image.gif\"      Square150x150Logo=\"Medium-Image.jpg\" /></Application>", false },
    {"<Application>  <VisualElements      BackgroundColor=\"aqua\"      ForegroundText=\"dark\"      ShowNameOnSquare150x150Logo=\"on\"      Square70x70Logo=\"Small-Image.Gif\"      Square150x150Logo=\"Medium-Image.jpeg\" /></Application>", false },
    {"<Application>  <VisualElements      BackgroundColor=\"aqua\"      ForegroundText=\"dark\"      ShowNameOnSquare150x150Logo=\"on\"      Square70x70Logo=\"\\Small-Image.gif\"      Square150x150Logo=\"Medium-Image.jpeg\" /></Application>", false },
    {"<Application>  <VisualElements      BackgroundColor=\"aqua\"      ForegroundText=\"dark\"      ShowNameOnSquare150x150Logo=\"on\"      Square70x70Logo=\"Images\\Small-Image.gif\"      Square150x150Logo=\"Medium-Image.jpeg\" /></Application>", true },
    {"<Application>  <VisualElements      BackgroundColor=\"aqua\"      ForegroundText=\"dark\"      ShowNameOnSquare150x150Logo=\"on\"      Square70x70Logo=\"C:\\Images\\Small-Image.gif\"      Square150x150Logo=\"Medium-Image.jpeg\" /></Application>", true }
};
var Results = TestFragments.Select((Pair, Index) => new KeyValuePair<int, bool>(Index++, Pair.Value == ManifestService.Validate(Pair.Key))).ToList();
            
Results.ForEach(Pair => Console.WriteLine("{0} : {1}", Pair.Key + 1, Pair.Value ? "PASSED" : "NOT PASSED"));
Console.WriteLine();
Console.WriteLine("Test: {0}", Results.All(Pair => Pair.Value)? "PASSED" : "NOT PASSED");

Console.ReadKey();
```

###
�

###### EXAMPLE OUTPUT
------------
```
1 : PASSED
2 : PASSED
3 : PASSED
4 : PASSED
5 : PASSED
6 : PASSED
7 : PASSED
8 : PASSED
9 : PASSED
10 : PASSED
11 : PASSED

Test: PASSED
```