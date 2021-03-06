<template>
    <div>
        <h2>--- Day 1: The Tyranny of the Rocket Equation ---</h2>
        <p>
            Santa has become stranded at the edge of the Solar System while delivering 
            presents to other planets! To accurately calculate his position in space, 
            safely align his warp drive, and return to Earth in time to save Christmas, 
            he needs you to bring him measurements from fifty stars.
        </p>
        <p>
            Collect stars by solving puzzles. Two puzzles will be made available on 
            each day in the Advent calendar; the second puzzle is unlocked when you 
            complete the first. Each puzzle grants one star. Good luck!
        </p>
        <h3>
            The Elves quickly load you into a spacecraft and prepare to launch.
        </h3>
        <p>
            At the first Go / No Go poll, every Elf is Go until the Fuel 
            Counter-Upper. They haven't determined the amount of fuel required yet.
        </p>
        <p>
            Fuel required to launch a given module is based on its mass. Specifically, 
            to find the fuel required for a module, take its mass, divide by three, 
            round down, and subtract 2.
        </p>
        <h4>For example:</h4>
        <p>
            For a mass of 12, divide by 3 and round down to get 4, then subtract 2 to get 2.
            For a mass of 14, dividing by 3 and rounding down still yields 4, so the fuel required is also 2.
            For a mass of 1969, the fuel required is 654.
            For a mass of 100756, the fuel required is 33583.
            The Fuel Counter-Upper needs to know the total fuel requirement. 
            To find it, individually calculate the fuel needed for the mass of each 
            module (your puzzle input), then add together all the fuel values.
        </p>
        <p>
            What is the sum of the fuel requirements for all of the modules on your spacecraft?
        </p>
        <p>
            (Enter number and hit enter)
        </p>
        <div class="submitSection">
            <input 
                @keyup.enter="calcFuel1(inputField)" 
                v-model="inputField" 
                type="text" 
                placeholder="Insert number & hit enter" 
                style="margin-bottom: 15px">
            
        </div>
        
        <h3>Solution: {{solution }}</h3>
        <h5>Your input: {{ inputField }}</h5>

        <h3>This is the solution for the entire dataset provided at the <a href="https://adventofcode.com/2019/day/1/input" target="_blank">/input</a></h3>
        <h3> {{ totalSolution }} </h3>
        <br>
        <h1>Part 2</h1>
        <h2>
            --- Part Two ---
        </h2>
        <p>
            During the second Go / No Go poll, the Elf in charge of the Rocket Equation Double-Checker 
            stops the launch sequence. Apparently, you forgot to include additional fuel for the fuel you 
            just added.

        </p>
        <p>
            Fuel itself requires fuel just like a module - take its mass, divide by three, round down, 
            and subtract 2. However, that fuel also requires fuel, and that fuel requires fuel, and so 
            on. Any mass that would require negative fuel should instead be treated as if it requires 
            zero fuel; the remaining mass, if any, is instead handled by wishing really hard, which 
            has no mass and is outside the scope of this calculation.
        </p>
        <p>
            So, for each module mass, calculate its fuel and add it to the total. Then, treat the fuel 
            amount you just calculated as the input mass and repeat the process, continuing until a fuel 
            requirement is zero or negative. For example:
        </p>
        <p>
            A module of mass 14 requires 2 fuel. This fuel requires no further fuel (2 divided by 3 and 
            rounded down is 0, which would call for a negative fuel), so the total fuel required is still 
            just 2.
        </p>
        <p>
            At first, a module of mass 1969 requires 654 fuel. Then, this fuel requires 216 more fuel 
            (654 / 3 - 2). 216 then requires 70 more fuel, which requires 21 fuel, which requires 5 fuel,
             which requires no further fuel. So, the total fuel required for a module of mass 1969 is 654 + 
             216 + 70 + 21 + 5 = 966.
        </p>
        <p>
            The fuel required by a module of mass 100756 and its fuel is: 33583 + 11192 + 3728 + 1240 + 
            411 + 135 + 43 + 12 + 2 = 50346.
            What is the sum of the fuel requirements for all of the modules on your spacecraft when also 
            taking into account the mass of the added fuel? (Calculate the fuel requirements for each module 
            separately, then add them all up at the end.)
        </p>
        <h2>Solution for Part 2</h2>
        <h3>This is the solution for the entire dataset provided at the <a href="https://adventofcode.com/2019/day/1/input" target="_blank">/input</a></h3>
        <br>
        <h3> {{ secondTotalSolution }} </h3>

        

    </div>
</template>

<script>
// import { TxtReader } from "txt-reader"
import input from 'raw-loader!../Inputs/input.txt'

export default {
    data: function () {
        return {
            modules: 14,
            inputField: 0,
            input: input,
            solution: 0,
            totalSolution: 0,
            secondTotalSolution: 0
        }
    },
    created:{
        },
        methods: {
            calcFuel1 (inputField) {
                return this.solution = Math.floor(inputField/3)-2
            },
            calcFuelneeded (mass) {
                return Math.floor(mass/3)-2
            },
            calcFuel (input) {
                let mass = input.split('\n').map(v => Number.parseInt(v))
                    this.totalSolution = mass.reduce((total, mass) => {return total + this.calcFuelneeded(mass)}, 0)
            },
            go () {
                let f = x => Math.floor(x / 3) - 2;
                let go = x => f(x) <= 0 ? 0 : f(x) + go(f(x));
                let run = func => input.split("\n").map(x => func(x)).reduce((a, b) => a + b);
                console.log(`Part 1: ${run(f)}\nPart 2: ${this.secondTotalSolution = run(go)}`);
            }
        },
        mounted () {
            this.calcFuel(input),
            this.go(input)
        }
}
</script>

<style  scoped>
    .submitSection {
        display: flex;
        justify-content: center;
        flex-direction: column;
        margin-right: 250px;
        margin-left: 250px;
    }
</style>