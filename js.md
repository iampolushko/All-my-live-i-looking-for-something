js - scenarios laguage. Не строготипизированный
It is makes possibe the actions on the page without restarging it, only on client side.

<noscript>User will see this block only if js is off in him browser</noscript>

<script>U can write code inside the</script> or connect another js file with <script src="reletive path/link here"></script>

var arr = new Array(1, 2, 3); and var arr = [4, 5, 6]; is equivalent
document.write(arr[number of element]);

var some_shit = anyt type shit; - variabe creating process.
document - global object what helps to controll the DOM structure(all html tags)

console - using to work with developer console in browser
have a methods .log/.info(same purpose), .error(scarry red exeption text), .warn(not to scary yellow colored text)

modal like windows (u can not customise it)
alert("Some thing"); - just alert window
confirm("Some thing"); - it is return the bool value
prompt("Some thing", b); - b is a "defoult" param, you can not add this

inside the html tag you can add any attribute onSomeShitHappend() like onclick(), onimput(). If we add parametr this in function <button onclick="someShitFuction(this)">Push the button</button>,
we take as argument the all html object, button in this case. In js file u need to someShitFuction(argument).

You can change the inner html text with argument.innerHTML = “New text”
You can change style with argument.style
