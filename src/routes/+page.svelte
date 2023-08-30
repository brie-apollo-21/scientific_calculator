<script>
    import Keypad from "../lib/components/Keypad.svelte";

    const keypadConfig = [
        ['x<sup>y</sup>','π','e','C','+'],
        ['√x','7','8','9','-'],
        ['<sup>1</sup>/<sub>x</sub>','4','5','6','×'],
        ['log','1','2','3','÷'],
        ['ln','<sup>+</sup>/<sub>-</sub>','0',',','=']
    ]
    const normalKeys = ['π','e','9','8','7','6','5','4','3','2','1','0',',','+','-','×','÷']

    function parseToJS(str) {
        str = String(str);
        str = str.replaceAll("×", "*");
        str = str.replaceAll("÷", "/");
        str = str.replaceAll(",", ".");
        str = str.replaceAll("π", "Math.PI");
        str = str.replaceAll("e", "Math.E");
        str = str.replaceAll("^", "**")
        return str;
    }

    function keyPressed(key) {
        let stream = document.getElementById("display").innerHTML;

        if(stream.length > 0) {
            switch(key) {
                case "C":
                    stream = "";
                    break;
                case "=":
                    stream = eval(parseToJS(stream));
                    break;
                case "log":
                    stream = Math.log10(eval(parseToJS(stream)));
                    break;
                case "ln":
                    stream = Math.log(eval(parseToJS(stream)));
                    break;
                case "<sup>+</sup>/<sub>-</sub>":
                    console.log(parseToJS(stream));
                    stream = eval(parseToJS(stream))*-1;
                    console.log(stream);
                    break;
                case "√x":
                    stream = Math.sqrt(eval(parseToJS(stream)));
                    break;
                case "<sup>1</sup>/<sub>x</sub>":
                    stream = eval("1/"+parseToJS(stream));
                    break;
                case "x<sup>y</sup>":
                    stream += '^'
                    break;
            }
        }
        if(normalKeys.includes(key)){
            if(key === 'π' || key === 'e'){
                if(!['0','1','2','3','4','5','6','7','8','9','e','π'].includes(stream[stream.length-1])) {
                    stream += key;
                }
            } else if(['+','-','×','÷'].includes(key)) {
                if(['0','1','2','3','4','5','6','7','8','9','π','e'].includes(stream[stream.length-1])) {
                    stream += key;
                }
            } else if(key === ',') {
                if(stream[stream.length-1] !== ',') {
                    stream += key;
                }
            } else if(['0','1','2','3','4','5','6','7','8','9'].includes(key)) {
                if(!stream[stream.length-1] === 'π' || !stream[stream.length-1] === 'e') {
                    stream += key;
                } else {
                    stream += key;
                }
            } 
        }

        document.getElementById("display").innerHTML = String(stream).replaceAll(".", ",");
    }
</script>

<div class="flex flex-col h-screen p-7 from-slate-100 to-slate-500 bg-gradient-to-bl justify-center select-none">
    <div class="flex from-slate-400 to-slate-600 bg-gradient-to-bl p-5 rounded-md mb-3 mx-auto h-1/4 w-full sm:w-4/5 md:w-3/4 shadow-2xl">
        <div class="from-slate-700 to-slate-800 bg-gradient-to-bl px-6 rounded-md flex-grow flex">
            <p id="display" class="text-slate-100 w-full my-auto align-middle tracking-wider text-3xl opacity-90" style="font-family: 'Inter Tight', sans-serif;"></p>
        </div>
    </div>
    <div id="keypad" class="from-slate-400 to-slate-600 bg-gradient-to-bl p-3 rounded-md my-3 w-full sm:w-4/5 md:w-3/4 mx-auto shadow-2xl">
        {#each keypadConfig as row}
            <div class="flex flex-row justify-center">
                {#each row as key}
                    <Keypad text={key} func={() => {keyPressed(key)}} />
                {/each}
            </div>
        {/each}
    </div>
    <a style="font-family: 'Inter Tight', sans-serif;" class="cursor-pointer text-slate-800 opacity-75 hover:opacity-100 duration-100 mx-auto text-center mt-3" href="https://github.com/Natalius-dev" target="_blank">Made by Natalius &#10084;</a>
</div>
