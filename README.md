[![Visitors](https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https%3A%2F%2Fgithub.com%2FRoyiAvital%2FStackExchangeCodes&count_bg=%2379C83D&title_bg=%23555555&icon=&icon_color=%23E7E7E7&title=Visitors+%28Daily+%2F+Total%29&edge_flat=false)](https://github.com/RoyiAvital/Julia100Exercises)

# Julia 100 Exercises

A set of introductory exercises for Julia. Based on [100 NumPy Exercises](https://github.com/rougier/numpy-100).

In order to generate this file:
1. Clone the repository (Or download).
2. Activate the project.
3. Run:
```Julia
using Literate;
Literate.markdown("Julia100Exercises.jl", name = "README", execute = true, flavor = Literate.CommonMarkFlavor());
```

**Remark**: Tested with Julia `1.7.2`.

````julia
using Literate;
using LinearAlgebra;
using Statistics;
using Dates;
using DelimitedFiles;
using UnicodePlots;
using Random;
````

## Question 001
Import the `LinearAlgebra` package under the name `LA`. (★☆☆)

````julia
import LinearAlgebra as LA;
````

## Question 002
Print the version of Julia. (★☆☆)

````julia
println(VERSION);
````

````
1.7.2

````

## Question 003
Create a non initialized vector of size 10 of `Float64`. (★☆☆)

````julia
vA = Vector{Float64}(undef, 10)
````

````
10-element Vector{Float64}:
 1.244556366e-314
 1.2563254363e-314
 1.32808859e-314
 1.256328314e-314
 1.2445621523e-314
 1.2445621997e-314
 1.2445622234e-314
 1.256328061e-314
 1.2563280924e-314
 1.256328124e-314
````

Which is equivalent of

````julia
vA = Array{Float64, 1}(undef, 10)
````

````
10-element Vector{Float64}:
 3.5e-323
 5.4e-323
 4.4e-323
 5.0e-323
 4.0e-323
 3.0e-323
 1.0e-323
 2.5e-323
 2.0e-323
 1.5e-323
````

## Question 004
Find the memory size of any array. (★☆☆)

````julia
sizeof(vA)
````

````
80
````

## Question 005
Show the documentation of the `+` (Add) method. (★☆☆)

````julia
@doc +
````

```
+(x, y...)
```

Addition operator. `x+y+z+...` calls this function with all arguments, i.e. `+(x, y, z, ...)`.

# Examples

```jldoctest
julia> 1 + 20 + 4
25

julia> +(1, 20, 4)
25
```

```
dt::Date + t::Time -> DateTime
```

The addition of a `Date` with a `Time` produces a `DateTime`. The hour, minute, second, and millisecond parts of the `Time` are used along with the year, month, and day of the `Date` to create the new `DateTime`. Non-zero microseconds or nanoseconds in the `Time` type will result in an `InexactError` being thrown.


## Question 006
Create a vector of zeros of size 10 but the fifth value which is 1. (★☆☆)

````julia
vA = zeros(10);
vA[5] = 1.0;
vA
````

````
10-element Vector{Float64}:
 0.0
 0.0
 0.0
 0.0
 1.0
 0.0
 0.0
 0.0
 0.0
 0.0
````

## Question 007
Create a vector with values ranging from 7 to 12. (★☆☆)

````julia
vA = 7:12
````

````
7:12
````

The above is efficient type. In order to explicitly create a vector:

````julia
vA = collect(7:12)
````

````
6-element Vector{Int64}:
  7
  8
  9
 10
 11
 12
````

## Question 008
Reverse a vector (first element becomes last). (★☆☆)

````julia
vA = collect(1:3);
vB = vA[end:-1:1];
vB
````

````
3-element Vector{Int64}:
 3
 2
 1
````

Alternative 001:

````julia
vB = reverse(vA);
````

Alternative 002 (In place):

````julia
reverse!(vA);
vA
````

````
3-element Vector{Int64}:
 3
 2
 1
````

## Question 009
Create a `3x3` matrix with values ranging from 0 to 8. (★☆☆)

````julia
mA = reshape(0:8, 3, 3)
````

````
3×3 reshape(::UnitRange{Int64}, 3, 3) with eltype Int64:
 0  3  6
 1  4  7
 2  5  8
````

Another way would be:

````julia
mA = Matrix{Float64}(undef, 3, 3);
mA[:] = 0:8;
````

## Question 010
Find indices of non zero elements from `[1, 2, 0, 0, 4, 0]`. (★☆☆)

````julia
findall(!iszero, [1, 2, 0, 0, 4, 0])
````

````
3-element Vector{Int64}:
 1
 2
 5
````

## Question 011
Create a 3x3 identity matrix. (★☆☆)

````julia
mA = I(3)
````

````
3×3 Diagonal{Bool, Vector{Bool}}:
 1  ⋅  ⋅
 ⋅  1  ⋅
 ⋅  ⋅  1
````

An alternative method (Explicit matrix) would be:

````julia
mA = Matrix(I, 3, 3) #<! For Float64: Matrix{Float64}(I, 3, 3)
````

````
3×3 Matrix{Bool}:
 1  0  0
 0  1  0
 0  0  1
````

## Question 012
Create a `2x2x2` array with random values. (★☆☆)

````julia
mA = randn(2, 2, 2)
````

````
2×2×2 Array{Float64, 3}:
[:, :, 1] =
 -0.635332  -0.666693
  0.678804  -1.31923

[:, :, 2] =
 -0.0408719  1.10664
  1.03166    0.195227
````

## Question 013
Create a `5x5` array with random values and find the minimum and maximum values. (★☆☆)

````julia
mA = rand(5, 5);
minVal = minimum(mA)
````

````
0.11510690212566976
````

````julia
maxVal = maximum(mA)
````

````
0.9992534828106966
````

Using `extrema()` one could get both values at once:

````julia
minVal, maxVal = extrema(mA);
````

## Question 014
Create a random vector of size 30 and find the mean value. (★☆☆)

````julia
meanVal = mean(randn(30))
````

````
-0.19787621300647687
````

## Question 015
Create a 2d array with 1 on the border and 0 inside. (★☆☆)

````julia
mA = zeros(4, 4);
mA[:, [1, end]] .= 1;
mA[[1, end], :] .= 1;
mA
````

````
4×4 Matrix{Float64}:
 1.0  1.0  1.0  1.0
 1.0  0.0  0.0  1.0
 1.0  0.0  0.0  1.0
 1.0  1.0  1.0  1.0
````

An alternative way:

````julia
mA = ones(4, 5);
mA[2:(end - 1), 2:(end - 1)] .= 0;
````

Using one line code:

````julia
mA = zeros(4, 5);
mA[[LinearIndices(mA)[cartIdx] for cartIdx in CartesianIndices(mA) if (any(cartIdx.I .== 1) || cartIdx.I[1] == size(mA, 1) || cartIdx.I[2] == size(mA, 2))]] .= 1;
````

## Question 016
Add a border of zeros around the array. (★☆☆)

````julia
mB = zeros(size(mA) .+ 2);
mB[2:(end - 1), 2:(end - 1)] = mA;
mB
````

````
6×7 Matrix{Float64}:
 0.0  0.0  0.0  0.0  0.0  0.0  0.0
 0.0  1.0  1.0  1.0  1.0  1.0  0.0
 0.0  1.0  0.0  0.0  0.0  1.0  0.0
 0.0  1.0  0.0  0.0  0.0  1.0  0.0
 0.0  1.0  1.0  1.0  1.0  1.0  0.0
 0.0  0.0  0.0  0.0  0.0  0.0  0.0
````

## Question 017
Evaluate the following expressions. (★☆☆)

````julia
0 * NaN
````

````
NaN
````

````julia
NaN == NaN
````

````
false
````

````julia
Inf > NaN
````

````
false
````

````julia
NaN - NaN
````

````
NaN
````

````julia
NaN in [NaN]
````

````
false
````

````julia
0.3 == 3 * 0.1
````

````
false
````

## Question 018
Create a `5x5` matrix with values `[1, 2, 3, 4]` just below the diagonal. (★☆☆)

````julia
mA = diagm(5, 5, -1 => 1:4)
````

````
5×5 Matrix{Int64}:
 0  0  0  0  0
 1  0  0  0  0
 0  2  0  0  0
 0  0  3  0  0
 0  0  0  4  0
````

## Question 019
Create a `8x8` matrix and fill it with a checkerboard pattern. (★☆☆)

````julia
mA = zeros(8, 8);
mA[2:2:end, 1:2:end] .= 1;
mA[1:2:end, 2:2:end] .= 1;
mA
````

````
8×8 Matrix{Float64}:
 0.0  1.0  0.0  1.0  0.0  1.0  0.0  1.0
 1.0  0.0  1.0  0.0  1.0  0.0  1.0  0.0
 0.0  1.0  0.0  1.0  0.0  1.0  0.0  1.0
 1.0  0.0  1.0  0.0  1.0  0.0  1.0  0.0
 0.0  1.0  0.0  1.0  0.0  1.0  0.0  1.0
 1.0  0.0  1.0  0.0  1.0  0.0  1.0  0.0
 0.0  1.0  0.0  1.0  0.0  1.0  0.0  1.0
 1.0  0.0  1.0  0.0  1.0  0.0  1.0  0.0
````

## Question 020
Convert the linear index 100 to a _Cartesian Index_ of a size `(6,7,8)`. (★☆☆)

````julia
mA = rand(6, 7, 8);
cartIdx = CartesianIndices(mA)[100]; #<! See https://discourse.julialang.org/t/14666
mA[cartIdx] == mA[100]
````

````
true
````

## Question 021
Create a checkerboard `8x8` matrix using the `repeat()` function. (★☆☆)

````julia
mA = repeat([0 1; 1 0], 4, 4)
````

````
8×8 Matrix{Int64}:
 0  1  0  1  0  1  0  1
 1  0  1  0  1  0  1  0
 0  1  0  1  0  1  0  1
 1  0  1  0  1  0  1  0
 0  1  0  1  0  1  0  1
 1  0  1  0  1  0  1  0
 0  1  0  1  0  1  0  1
 1  0  1  0  1  0  1  0
````

## Question 022
Normalize a `4x4` random matrix. (★☆☆)

````julia
mA = rand(4, 4);
mA .= (mA .- mean(mA)) ./ std(mA) #<! Pay attention that `@.` will yield error (`std()` and `mean()`)
````

````
4×4 Matrix{Float64}:
 -1.3305     0.699109   1.11255    0.280731
  0.878488  -0.480009  -1.53652   -1.10125
  0.769686   1.3316    -0.427922  -1.45437
  0.651932   0.946513  -0.804871   0.464831
````

## Question 023
Create a custom type that describes a color as four unsigned bytes (`RGBA`). (★☆☆)

````julia
struct sColor
    R::UInt8;
    G::UInt8;
    B::UInt8;
    A::UInt8;
end

sMyColor = sColor(rand(UInt8, 4)...)
````

````
Main.##374.sColor(0x20, 0xe1, 0x86, 0x56)
````

## Question 024
Multiply a `2x4` matrix by a `4x3` matrix. (★☆☆)

````julia
mA = rand(2, 4) * randn(4, 3)
````

````
2×3 Matrix{Float64}:
 -2.87746   0.402955  -0.0942266
 -2.67299  -0.646446   0.618675
````

## Question 025
Given a 1D array, negate all elements which are between 3 and 8, in place. (★☆☆)

````julia
vA = rand(1:10, 8);
map!(x -> ((x > 3) && (x < 8)) ? -x : x, vA, vA)
````

````
8-element Vector{Int64}:
  2
  3
  9
 -5
 -6
 -6
  8
 -6
````

Using logical indices one could use:

````julia
vA[3 .< vA .< 8] .*= -1;
````

## Question 026
Sum the array `1:4` with initial value of -10. (★☆☆)

````julia
sum(1:4, init = -10)
````

````
0
````

## Question 027
Consider an integer vector `vZ` validate the following expressions. (★☆☆)
```julia
vZ .^ vZ
2 << vZ >> 2
vZ <- vZ
1im * vZ
vZ / 1 / 1
vZ < Z > Z
```

````julia
vZ = rand(1:10, 3);
````

````julia
vZ .^ vZ
````

````
3-element Vector{Int64}:
   256
 46656
     1
````

````julia
try
    2 << vZ >> 2
catch e
    println(e)
end
````

````
MethodError(<<, (2, [4, 6, 1]), 0x0000000000007d21)

````

````julia
vZ <- vZ
````

````
false
````

````julia
1im * vZ
````

````
3-element Vector{Complex{Int64}}:
 0 + 4im
 0 + 6im
 0 + 1im
````

````julia
vZ / 1 / 1
````

````
3-element Vector{Float64}:
 4.0
 6.0
 1.0
````

````julia
vZ < vZ > vZ
````

````
false
````

## Question 028
Evaluate the following expressions. (★☆☆)

````julia
[0] ./ [0]
````

````
1-element Vector{Float64}:
 NaN
````

````julia
try
    [0] .÷ [0]
catch e
    println(e)
end
````

````
DivideError()

````

````julia
try
    convert(Float, convert(Int, NaN))
catch e
    println(e)
end
````

````
InexactError(:Int64, Int64, NaN)

````

## Question 029
Round away from zero a float array. (★☆☆)

````julia
vA = randn(10);
map(x -> x > 0 ? ceil(x) : floor(x), vA)
````

````
10-element Vector{Float64}:
 -1.0
  1.0
  2.0
  1.0
 -1.0
  1.0
 -1.0
 -1.0
 -1.0
  1.0
````

## Question 030
Find common values between two arrays. (★☆☆)

````julia
vA = rand(1:10, 6);
vB = rand(1:10, 6);

vA[findall(in(vB), vA)]
````

````
5-element Vector{Int64}:
 8
 6
 8
 2
 6
````

## Question 031
Suppress Julia's warnings. (★☆☆)

One could use [Suppressor.jl](https://github.com/JuliaIO/Suppressor.jl).

## Question 032
Compare `sqrt(-1)` and `sqrt(-1 + 0im)`. (★☆☆)

````julia
try
    sqrt(-1)
catch e
    println(e)
end
````

````
DomainError(-1.0, "sqrt will only return a complex result if called with a complex argument. Try sqrt(Complex(x)).")

````

````julia
sqrt(-1 + 0im)
````

````
0.0 + 1.0im
````

## Question 033
Display yesterday, today and tomorrow's date. (★☆☆)

````julia
println("Yesterday: $(today() - Day(1))");
println("Today: $(today())");
println("Tomorrow: $(today() + Day(1))");
````

````
Yesterday: 2022-03-30
Today: 2022-03-31
Tomorrow: 2022-04-01

````

## Question 034
Display all the dates corresponding to the month of July 2016. (★★☆)

````julia
collect(Date(2016,7,1):Day(1):Date(2016,7,31))
````

````
31-element Vector{Date}:
 2016-07-01
 2016-07-02
 2016-07-03
 2016-07-04
 2016-07-05
 2016-07-06
 2016-07-07
 2016-07-08
 2016-07-09
 2016-07-10
 2016-07-11
 2016-07-12
 2016-07-13
 2016-07-14
 2016-07-15
 2016-07-16
 2016-07-17
 2016-07-18
 2016-07-19
 2016-07-20
 2016-07-21
 2016-07-22
 2016-07-23
 2016-07-24
 2016-07-25
 2016-07-26
 2016-07-27
 2016-07-28
 2016-07-29
 2016-07-30
 2016-07-31
````

## Question 035
Compute `((mA + mB) * (-mA / 2))`` in place. (★★☆)

````julia
mA = rand(2, 2);
mB = rand(2, 2);
mA .= ((mA .+ mB) .* (.-mA ./ 2))
````

````
2×2 Matrix{Float64}:
 -0.299773   -0.211908
 -0.0885477  -0.0879553
````

Using the dot macro:

````julia
@. mA = ((mA + mB) * (-mA / 2));
````

## Question 036
Extract the integer part of a random array of positive numbers using 4 different methods. (★★☆)

````julia
mA = 5 * rand(3, 3);
````

Option 1:

````julia
floor.(mA)
````

````
3×3 Matrix{Float64}:
 4.0  0.0  3.0
 3.0  0.0  4.0
 1.0  0.0  1.0
````

Option 2:

````julia
round.(mA .- 0.5) #<! Generates -0.0 for numbers smaller than 0.5
````

````
3×3 Matrix{Float64}:
 4.0  0.0  3.0
 3.0  0.0  4.0
 1.0  0.0  1.0
````

Option 3:

````julia
mA .÷ 1
````

````
3×3 Matrix{Float64}:
 4.0  0.0  3.0
 3.0  0.0  4.0
 1.0  0.0  1.0
````

Option 4:

````julia
mA .- rem.(mA, 1)
````

````
3×3 Matrix{Float64}:
 4.0  0.0  3.0
 3.0  0.0  4.0
 1.0  0.0  1.0
````

## Question 037
Create a `5x5` matrix with row values ranging from 0 to 4. (★★☆)

````julia
mA = repeat(reshape(0:4, 1, 5), 5, 1)
````

````
5×5 Matrix{Int64}:
 0  1  2  3  4
 0  1  2  3  4
 0  1  2  3  4
 0  1  2  3  4
 0  1  2  3  4
````

## Question 038
Generate an array using a generator of 10 numbers. (★☆☆)

````julia
vA = collect(x for x in 1:10)
````

````
10-element Vector{Int64}:
  1
  2
  3
  4
  5
  6
  7
  8
  9
 10
````

## Question 039
Create a vector of size 10 with values ranging from 0 to 1, both excluded. (★★☆)

````julia
vA = LinRange(0, 1, 12)[2:(end - 1)]
````

````
10-element LinRange{Float64, Int64}:
 0.0909091,0.181818,0.272727,0.363636,…,0.636364,0.727273,0.818182,0.909091
````

## Question 040
Create a random vector of size 10 and sort it. (★★☆)

````julia
vA = rand(1:10, 10);
sort(vA)
````

````
10-element Vector{Int64}:
  1
  1
  1
  3
  3
  4
  6
  6
  8
 10
````

## Question 041
Implement the `sum()` function manually. (★★☆)

````julia
vA = rand(100);
sumVal = vA[1]
for ii in 2:length(vA)
    global sumVal += vA[ii];
end
````

## Question 042
Check for equality of 2 arrays. (★★☆)

````julia
vA = rand(10);
vB = rand(10);

all(vA .== vB)
````

````
false
````

## Question 043
Make an array immutable (Read only). (★★☆)

This is a work in progress for Julia at in [Issue 31630](https://github.com/JuliaLang/julia/pull/31630).

## Question 044
Consider a random `10x2` matrix representing cartesian coordinates, convert them to polar coordinates. (★★☆)

````julia
mA = rand(10, 2);

ConvToPolar = vX -> [hypot(vX[1], vX[2]), atan(vX[2], vX[1])]

mB = [ConvToPolar(vX) for vX in eachrow(mA)]
````

````
10-element Vector{Vector{Float64}}:
 [0.7723926362093879, 0.33773329944836106]
 [1.1218287191114062, 0.9629139493843093]
 [1.056848940096086, 0.8685636983939284]
 [0.3970403769905774, 1.3068052888331851]
 [0.7003935274611301, 0.3153866199915688]
 [0.983507059118245, 0.8025499982013847]
 [0.5813275476803443, 0.6658667605908044]
 [0.9713543766132763, 1.0633408580655896]
 [1.3753025059720887, 0.7962313234608916]
 [0.23951207795938909, 1.4349666434209103]
````

## Question 045
Create random vector of size 10 and replace the maximum value by 0. (★★☆)

````julia
vA = randn(10);
vA[argmax(vA)] = 0;
vA
````

````
10-element Vector{Float64}:
  0.46190010274373217
 -0.41503183394367327
 -0.7549488290385445
  0.7552436567390878
 -1.1076835080187921
  0.9397973787756825
  0.0
 -1.473002812695306
 -0.8912173725607507
 -0.27051460100335917
````

## Question 046
Create a a grid of `x` and `y` coordinates covering the `[0, 1] x [0, 1]` area. (★★☆)

````julia
numGridPts = 5;
vX = LinRange(0, 1, numGridPts);
vY = LinRange(0, 1, numGridPts);
MeshGrid = (vX, vY) -> ([x for _ in vY, x in vX], [y for y in vY, _ in vX]);

mX, mY = MeshGrid(vX, vY); #<! See https://discourse.julialang.org/t/48679
@show mX
````

````
5×5 Matrix{Float64}:
 0.0  0.25  0.5  0.75  1.0
 0.0  0.25  0.5  0.75  1.0
 0.0  0.25  0.5  0.75  1.0
 0.0  0.25  0.5  0.75  1.0
 0.0  0.25  0.5  0.75  1.0
````

````julia
@show mY
````

````
5×5 Matrix{Float64}:
 0.0   0.0   0.0   0.0   0.0
 0.25  0.25  0.25  0.25  0.25
 0.5   0.5   0.5   0.5   0.5
 0.75  0.75  0.75  0.75  0.75
 1.0   1.0   1.0   1.0   1.0
````

## Question 047
Given two vectors, `vX`` and `vY``, construct the Cauchy matrix `mC`: `(Cij = 1 / (xi - yj))`. (★★☆)

````julia
vX = rand(5);
vY = rand(5);

mC = 1 ./ (vX .- vY')
````

````
5×5 Matrix{Float64}:
 26.0596    2.15501  -14.5645      1.2317    4.11926
 -6.28292   3.75234   -3.75664     1.62773  22.1108
 -2.76452  15.6409    -2.13329     2.42845  -6.35573
 -1.28181  -2.82098   -1.12716  -150.698    -1.73684
 -1.58249  -4.84844   -1.35328     7.06221  -2.33904
````

## Question 048
Print the minimum and maximum representable value for each Julia scalar type. (★★☆)

````julia
vT = [UInt8 UInt16 UInt32 UInt64 Int8 Int16 Int32 Int64 Float16 Float32 Float64]

for juliaType in vT
    println(typemin(juliaType));
    println(typemax(juliaType));
end
````

````
0
255
0
65535
0
4294967295
0
18446744073709551615
-128
127
-32768
32767
-2147483648
2147483647
-9223372036854775808
9223372036854775807
-Inf
Inf
-Inf
Inf
-Inf
Inf

````

## Question 049
Print all the values of an array. (★★☆)

````julia
mA = rand(3, 3);
print(mA);
````

````
[0.8089037067522848 0.4232665075041424 0.2140039268031556; 0.8705154803856733 0.676686097068589 0.6885533928213902; 0.9739196932164245 0.11476024028812004 0.0007902917516156016]
````

## Question 050
Find the closest value to a given scalar in a vector. (★★☆)

````julia
inputVal = 0.5;
vA = rand(10);

vA[argmin(abs.(vA .- inputVal))]
````

````
0.4843468613109032
````

## Question 051
Create a structured array representing a position `(x, y)` and a color `(r, g, b)`. (★★☆)

````julia
struct sPosColor
    x::Int
    y::Int
    R::UInt8;
    G::UInt8;
    B::UInt8;
    A::UInt8;
end

numPixels   = 10;
maxVal      = typemax(UInt32);
vMyColor    = [sPosColor(rand(1:maxVal, 2)..., rand(UInt8, 4)...) for _ in 1:numPixels];
````

## Question 052
Consider a random vector with shape `(5, 2)` representing coordinates, find the distances matrix `mD`: $ {D}_{i, j} = {\left\| {x}_{i} - {x}_{j} \right\|}_{2} $. (★★☆)

````julia
mX = rand(5, 2);
vSumSqr = sum(vX -> vX .^ 2, mX, dims = 2);
mD = vSumSqr .+ vSumSqr' - 2 * (mX * mX');
mD
````

````
5×5 Matrix{Float64}:
 0.0        0.468486  0.330388  0.517509  0.0427779
 0.468486   0.0       0.120198  0.54091   0.263447
 0.330388   0.120198  0.0       0.15222   0.135478
 0.517509   0.54091   0.15222   0.0       0.314189
 0.0427779  0.263447  0.135478  0.314189  0.0
````

## Question 053
Convert a float (32 bits) array into an integer (32 bits) in place. (★★☆)

````julia
vA = 100 .* rand(Float32, 5);
vA .= round.(Int32, vA)
````

````
5-element Vector{Float32}:
 37.0
 75.0
 48.0
  8.0
 44.0
````

## Question 054
Read the following file (`Q0054.txt`). (★★☆)
```
1, 2, 3, 4, 5
6,  ,  , 7, 8
 ,  , 9,10,11
```

````julia
mA = readdlm("Q0054.txt", ',')
````

````
3×5 Matrix{Any}:
 1     2      3       4   5
 6      "  "   "  "   7   8
  " "   "  "  9      10  11
````

## Question 055
Enumerate array in a loop. (★★☆)

````julia
mA = rand(3, 3);

for (elmIdx, elmVal) in enumerate(mA) #<! See https://discourse.julialang.org/t/48877
    println(elmIdx);
    println(elmVal);
end
````

````
1
0.5548376575373358
2
0.9109255659225378
3
0.5810315326123449
4
0.7182671657845195
5
0.6107042965530706
6
0.7026731069349421
7
0.9051744423034807
8
0.03459101266733211
9
0.5589179678203583

````

## Question 056
Generate a generic 2D Gaussian like array with `μ = 0`, `σ = 1` and indices over `{-5, -4, ..., 0, 1, ..., 5}`. (★★☆)

````julia
vA = -5:5;
μ = 0;
σ = 1;
mG = [(1 / (2 * pi * σ)) * exp(-0.5 * ((([x, y] .- μ)' * ([x, y] .- μ)) / (σ * σ))) for x in vA, y in vA];

heatmap(mG)
````

````
      ┌───────────┐              
   11 │▄▄▄▄▄▄▄▄▄▄▄│  ┌──┐ 0.2    
      │▄▄▄▄▄▄▄▄▄▄▄│  │▄▄│        
      │▄▄▄▄▄▄▄▄▄▄▄│  │▄▄│        
      │▄▄▄▄▄▄▄▄▄▄▄│  │▄▄│        
      │▄▄▄▄▄▄▄▄▄▄▄│  │▄▄│        
    1 │▄▄▄▄▄▄▄▄▄▄▄│  └──┘ 2.0e-12
      └───────────┘              
       1        11               
````

Using the separability of the Gaussian function:

````julia
vG = (1 / (sqrt(2 * pi) * σ)) .* exp.(-0.5 .* (((vA .- μ) .^ 2) / (σ * σ)));
mG = vG * vG';
````

## Question 057
Place `5` elements in a `5x5` array randomly. (★★☆)

````julia
mA = rand(5, 5);
mA[rand(1:25, 5)] = rand(5);
````

Another option which avoids setting into the same indices:

````julia
mA[randperm(25)[1:5]] = rand(5);
````

## Question 058
Subtract the mean of each row of a matrix. (★★☆)

````julia
mA = rand(3, 3);
mA .-= mean(mA, dims = 2);
mean(mA, dims = 1)
````

````
1×3 Matrix{Float64}:
 -0.0218399  -0.0652094  0.0870493
````

## Question 059
Sort an array by a column. (★★☆)

````julia
colIdx = 2;

mA = rand(3, 3);
mA[sortperm(mA[:, colIdx]), :]
````

````
3×3 Matrix{Float64}:
 0.446028  0.16373   0.899526
 0.805303  0.619357  0.0217868
 0.741157  0.821589  0.564293
````

Using `sortslices()`:

````julia
sortslices(mA, dims = 1, by = x -> x[colIdx]);
````

## Question 060
Tell if a given 2D array has null (All zeros) columns. (★★☆)

````julia
mA = rand(0:1, 3, 9);
any(all(iszero.(mA), dims = 1))
````

````
false
````

---

*This page was generated using [Literate.jl](https://github.com/fredrikekre/Literate.jl).*

