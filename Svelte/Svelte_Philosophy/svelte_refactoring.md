[16:06, 9/15/2021] Bernie: they actually come either from missing / faulty data that I get from the server - or - stem from "hyperreactivity" (as I call it)
[16:07, 9/15/2021] Bernie: all modern web development frameworks are reactive, so when certain conditions change, they automatically react and re-compute things
[16:08, 9/15/2021] Bernie: those re-computations can become pretty long cascades... and sometimes you get unwanted effects because there are causes you haven't forseen
[16:08, 9/15/2021] Bernie: I guess it's just a matter of crafting a really clear architecture
[16:10, 9/15/2021] Sergina: Oh okay okay. Got it! Thanks for explaining that. 😄 But how will you fix this kind of problem in the program?
[16:11, 9/15/2021] Bernie: first I should do a really long and hard refactoring session - making sure that the dependency graph between data has no cycles (= is topologically sorted)
[16:12, 9/15/2021] Bernie: then disentangle similar procedures by giving them their own data-structures instead of sharing
[16:13, 9/15/2021] Bernie: in my specific case, I'll also have to change some reactive properties into more formal reactive stores, cause I fear the framework I am using is doing more / behaving differently in the background than I assume
[16:14, 9/15/2021] Bernie: but I guess refactoring (= re-writing code to make it cleaner, more abstract, better encapsulated etc. without changing the functionality) will be enough to clear stuff up
[16:15, 9/15/2021] Bernie: also, I could extract all Dicom-related functionality (Dicom is a medical imaging and communication standard) out into a separate library...
[16:16, 9/15/2021] Bernie: and of course writing more documentation for each module + an extensive test suite which runs all the functionality on every change and immediately signals if anything went wrong (again)
[16:23, 9/15/2021] Sergina: So everything really starts and going back to refactoring when there's a problem?
[16:23, 9/15/2021] Bernie: no, sometimes you can immediately see a fix
[16:24, 9/15/2021] Bernie: refactoring is the suitable approach when problems start occurring because a code-base has grown "organically" for too long and thus become too complex, so you cannot easily see all interrelated effects anymore
