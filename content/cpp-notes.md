+++
title = 'C++ Notes'
date = 2024-10-04T16:44:00-06:00
draft = false
description = "General notes and basics for the C++ programming language"
image = "/images/cpp-logo.webp"
categories = ["c++", "sdl"]
authors = ["Skye Waddell"]
avatar = "/images/avatar.webp"
+++

# C++ Notes

# iostream
The <iostream> library provides objects which can read user input and output data to the console or to a file.

```cpp
#include <iostream>

cerr //output stream for error messages
clog //output stream to log program info
cin  //input stream that reads keyboard input from the console
cout //output stream which writes output to console
```
---
# fstream
The <fstream> library provides classes for reading and writing into files or data streams.

```cpp
#include <fstream>

filebuf  //lower level file handling class used internally by fstream, ifstream, and ofstream classes
fstream  //a class that can read and write to files
ifstream //a class that can read from files
ofstream //a class that can write to files
```
---
# cmath
The <cmath> library has many functions that allow you to perform mathematical tasks on numbers.

```cpp
#include <cmath>
erfc(x);    // Returns the value of the complementary error function at x
fabs(x);    // Returns the absolute value of a floating-point x
fdim(x, y); // Returns the positive difference between x and y
floor(x);   // Returns the value of x rounded down to its nearest integer
fma(x, y, z); // Returns x*y+z without losing precision
fmax(x, y); // Returns the highest value of a floating-point x and y
fmin(x, y); // Returns the lowest value of a floating-point x and y
fmod(x, y); // Returns the floating point remainder of x/y
frexp(x, y); // With x expressed as m*2^n, returns the value of m (0.5 to 1.0) and writes n to memory at y
hypot(x, y); // Returns sqrt(x² + y²) without intermediate overflow/underflow
ilogb(x);   // Returns the integer part of the floating-point base logarithm of x
ldexp(x, y); // Returns x * 2^y
lgamma(x);  // Returns the logarithm of the absolute value of the gamma function at x
llrint(x);  // Rounds x to a nearby integer and returns as long long int
llround(x); // Rounds x to the nearest integer and returns as long long int
log(x);     // Returns the natural logarithm of x
log10(x);   // Returns the base 10 logarithm of x
log1p(x);   // Returns the natural logarithm of x+1
log2(x);    // Returns the base 2 logarithm of the absolute value of x
logb(x);    // Returns the floating-point base logarithm of the absolute value of x
lrint(x);   // Rounds x to a nearby integer and returns as long int
lround(x);  // Rounds x to the nearest integer and returns as long int
modf(x, y); // Returns the decimal part of x and writes the integer part to memory at y
nan(s);     // Returns a NaN (Not a Number) value
nearbyint(x); // Returns x rounded to a nearby integer
nextafter(x, y); // Returns the closest floating-point number to x in the direction of y
nexttoward(x, y); // Returns the closest floating-point number to x in the direction of y
pow(x, y);  // Returns the value of x to the power of y
remainder(x, y); // Returns the remainder of x/y rounded to the nearest integer
remquo(x, y, z); // Calculates x/y rounded to nearest integer, writes to memory at z, returns remainder
rint(x);    // Returns x rounded to a nearby integer
round(x);   // Returns x rounded to the nearest integer
scalbln(x, y); // Returns x * R^y (R usually 2)
scalbn(x, y); // Returns x * R^y (R usually 2)
sin(x);     // Returns the sine of x (in radians)
sinh(x);    // Returns the hyperbolic sine of x
sqrt(x);    // Returns the square root of x
tan(x);     // Returns the tangent of x (in radians)
tanh(x);    // Returns the hyperbolic tangent of x
tgamma(x);  // Returns the value of the gamma function at x
trunc(x);   // Returns the integer part of x

```

---

# string
The <string> library has many functions that allow you to perform tasks on strings.

```cpp
#include <string>
at(index);       // Returns an indexed character from a string
length();        // Returns the length of a string
size();          // Alias of length(). Returns the length of a string
max_size();      // Returns the maximum length of a string
empty();         // Checks whether a string is empty or not
append(str);     // Appends a string (or a part of a string) to another string
substr(pos, len); // Returns a part of a string from a start index (position) and length
find(str);       // Returns the index (position) of the first occurrence of a string or character
rfind(str);      // Returns the index (position) of the last occurrence of a string or character
replace(pos, len, str); // Replaces a part of a string with another string
insert(pos, str); // Inserts a string at a specified index (position)
erase(pos, len);  // Removes characters from a string
compare(str);     // Compares two strings

```

---

# cstring
The <cstring> library has many functions that allow you to perform tasks on arrays and C-style strings.

Note that C-style strings are different than regular strings. A C-style string is an array of characters, created with the char type.

```cpp
#include <cstring>
memchr(ptr, value, num);   // Returns a pointer to the first occurrence of a value in a block of memory
memcmp(ptr1, ptr2, num);   // Compares two blocks of memory to determine which one represents a larger numeric value
memcpy(dest, src, num);    // Copies data from one block of memory to another
memmove(dest, src, num);   // Copies data from one block of memory to another, accounting for memory overlap
memset(ptr, value, num);   // Sets all of the bytes in a block of memory to the same value
strcat(dest, src);         // Appends one C-style string to the end of another
strchr(str, ch);           // Returns a pointer to the first occurrence of a character in a C-style string
strcmp(str1, str2);        // Compares the ASCII values of characters in two C-style strings to determine which has a higher value
strcoll(str1, str2);       // Compares the locale-based values of characters in two C-style strings to determine which has a higher value
strcpy(dest, src);         // Copies the characters of a C-style string into the memory of another string
strcspn(str1, str2);       // Returns the length of a C-style string up to the first occurrence of one of the specified characters
strerror(errnum);          // Returns a C-style string describing the meaning of an error code
strlen(str);               // Returns the length of a C-style string
strncat(dest, src, num);   // Appends a number of characters from a C-style string to the end of another string
strncmp(str1, str2, num);  // Compares the ASCII values of a specified number of characters in two C-style strings
strncpy(dest, src, num);   // Copies a number of characters from one C-style string into the memory of another string
strpbrk(str1, str2);       // Returns a pointer to the first position in a C-style string that contains one of the specified characters
strrchr(str, ch);          // Returns a pointer to the last occurrence of a character in a C-style string
strspn(str1, str2);        // Returns the length of a C-style string up to the first character not in the specified set
strstr(str1, str2);        // Returns a pointer to the first occurrence of a C-style string within another string
strtok(str, delim);        // Splits a string into pieces using delimiters
strxfrm(dest, src, num);   // Converts characters in a C-style string from ASCII encoding to the encoding of the current locale
```

---

# ctime
The <ctime> library has a variety of functions that allow you to measure dates and times.

```cpp
#include <ctime>
asctime(tm);          // Returns a C-style string representation of the time in a tm structure
clock();              // Returns a number representing the amount of time that has passed while the program is running
ctime(timestamp);    // Returns a C-style string representation of the time in a timestamp
difftime(time1, time2); // Returns the time difference between two timestamps
gmtime(timestamp);   // Converts a timestamp into a tm structure representing its time at the GMT time zone
localtime(timestamp); // Converts a timestamp into a tm structure representing its time in the system's local time zone
mktime(tm);          // Converts a tm structure into a timestamp
strftime(buffer, maxsize, format, tm); // Writes a C-style string representing the date and time of a tm structure with formatting options
time(nullptr);       // Returns a timestamp representing the current moment in time
```
---
# Types
```cpp
int //10
double //5.75
bool //true-false
char //single character/letter/number/ascii
std::string // "the default string"

const int POWER = 100; //constant variables (use CAPS for consts)
```
---
# Switch Statement
```cpp
switch(state){
    default:
    case "Hello":
        //state hello
    break;
    case "Goodbye":
        //state goodbye
    break;

```
---
# Loops
```cpp
//for
for (int i = 0; i < 5; i++) {
    cout << i << "\n";
}

//while
int i = 0;
while (i < 5) {
    cout << i << "\n";
    i++;
}

//do while
int i = 0;
do {
    cout << i << "\n";
    i++;
}
while (i < 5);

break; //breaks loop
continue; //continues loop
```
---
# Arrays
```cpp
//define an array
std::string cars[4] = { "Volvo", "BMW", "Ford", "Mazda" };
std::cout << cars[0]; //prints Volvo

//get size of an array
int arraySize = sizeof(cars)/sizeof(cars[0]

//2d array
std::string[2][4] = {
    { "A", "B", "C", "D" },
    { "E", "F", "G", "H" }
};
```
---
# Structs
Similar to an object, these can be used when oop is not needed for a simple data object.
```cpp
//define the structure
struct Player {
    std::string name;
    int hp;
    int level;
};

//create instance of struct and define its values
Player player;
player.name = "Skye";
player.hp = 100;
player.level = 5;
```
---
# Casting Struct to a Function
If you are trying to modify the original values of the struct you passed into the function, you must also use the address-of operator &.
```cpp
//define struct
struct Car {
    std::string model;
    int year;
    std::string color;
};

void printCar(Car &car); //declare function

//main duh
int main(){
    //create objects of the struct
    Car car1;
    Car car2;

    //define car1
    car1.model = "Honda";
    car1.year = 1997;
    car1.color = "white";

    //define car2
    car2.model = "Nissan";
    car2.year = 2002;
    car2.color = "black";

    printCar(car1);

    return 0;
}

//define print car function
void printCar(Car &car){
    std::cout << car.model;
    std::cout << car.year;
    std::cout << car.color;
}
```
---
# Enums
Enumerations are lists of data you can use to save memory space, and organize data with names.
```cpp
//define the enum
enum Level {
    LOW,    //0
    MEDIUM, //1
    HIGH    //2
}; 

//set a variable to the enum value
enum Level myLevel = MEDIUM;
```
# Pointers
A pointer is a variable that stores the MEMORY ADDRESS of another variable. This allows you to directly manipulate memory and work with data directly.

Analogy: Instead of going door-to-door with 20 free pizzas, its easier to just tell people where the free pizza is.

Pointers are often used in game dev when working with memory, large objects or interacting with graphics API's.
```cpp
std::string name = "Skye";
std:string *pName = &name; //create a pointer, with a reference to the name variable

std::cout << pName; //prints 0xff99eeb90
std::cout << *pName; //prints Skye
```
## When to use a pointer?
When you need to allocate memory dynamically.
Example: Creating objects, or arrays whose sizes are determined at runtime.
```cpp
Enemy* enemies = new Enemy[10];
delete[] enemies //make sure to free up memory
```
---

# Dynamic Memory
Memory that is allocated after the program is already compiled and running.
Use the 'new' operator to allocate memory in the heap rather than the stack.

useful when we don't know how much memory we will need. Makes our programs much more flexible especially when accepting user input.

For example:
```cpp
int *pNum = NULL;
pNum = new int;

*pNum = 21;
std::cout << pNum; //prints 0xff99cc
std::cout << *pNum; //print 21

//make sure to use the delete operator if using the new operator
delete pNum;
```
---

# Pointers with Arrays
When working with pointers and arrays, its good to be cognitive that using the address-of operator on an array will return its memory address!
```cpp
std::string freePizzas[5] = { "1","2","3","4","5" };
std::string *pFreePizzas = &freePizzas;

//The above code will throw an error because freePizzas is already pointing to a memory address!
std::cout << freePizzas; //prints 0xff99c88c
```
So you can just pass the array to pointer, with the address-of operator.
```cpp
std::string *pFreePizzas = freePizzas;

std::cout << pFreePizzas; //prints 0xff99cc
std::cout << *pFreePizzas; //prints 1 (the first element in the array)
```
---

# Null Pointers
A special value that means something has no value.
When a pointer is holding a null value that pointer is not pointing at anything (null pointer).
Null pointers are helpful when determining if an address was successfully assigned to a pointer.
```cpp
nullptr //keyword that represents a null pointer literal
```
Lets show some example of null pointers below. You usually use these when defining pointer addresses that don't yet have data to be stored in it.
```cpp
int *pointer = nullptr; //init a memory address, that doesnt yet have data
int x  123;

*pointer = &x;

//validate pointer assignment
if(pointer == nullptr){
    std::cout << "Address was NOT assigned!";
} else {
    std::cout << "Address was assigned";
    std::cout << *pointer; //prints 123
}
```
---

# References
A reference is an alias to another variable, meaning it refers to an existing variable.

Once a reference is initialized to a variable, it cannot be changed to another variable.
References are generally easier and safer to use than pointers because they are guaranteed to point to valid data (not null).
References will also automatically update themselves whenever the variable they are referencing changes.
```cpp
int x = 10;
int& ref = x;

std::cout << ref; //prints 10
ref = 20;
std::cout << x; //prints 20
```
### When to use a reference to a variable?
Example: when passing objects like Player or Enemy to a function that will manipulate them, it's often better to use references because the object is already created and guaranteed to exist.
References make it more readable and don't require pointer syntax (->)
```cpp
void updatePosition(Player& player) {
    player.x += 10;
}
```
---

# Passing by Value vs Reference
Next we have to discuss passing by reference when creating functions. Check out the following code which initializes some variables and prints their data
```cpp
std::string x = "Kool-Aid";
std::string y = "Water";

std::cout << x; //print Kool-Aid
std::cout << y; //print Water
```
All seems normal correct? It is printing the variables, now lets try making a function that requires x and y.
```cpp
void swap(std::string x, std::string y){
    std::string temp;
    temp = x;
    x = x;
    y = temp;
}
```
Okay cool, all is still well now lets try invoking this function and see what happens :)
```cpp
swap(x,y);
std::cout << x; //still prints Kool-Aid
std::cout << y; //still prints Water
```
So what happened, is when you passed x and y into the swap function, it merely made copies of those variables and it didn't actually modify the original variables at all. This is a quirk of c++ you will have to get used to.

If you need to change the original values, you need to pass the variables by reference.

Example:
```cpp
void swap(std::string &x, std::string &y){
    std::string temp;
    temp = x;
    x = y;
    y = temp;
}
```
Now when we will call swap with x and y, it will update the original variables values and not the copies.
```cpp
swap(x,y);
std::cout << x; //prints Water
std::cout << y; //prints Kool-Aids
```
---

# Memory Address
A location in memory where data is stored.
Memory addresses can be accessed with & (address-of operator).
```cpp
std::string name = "Skye";
std::cout << &name; //prints 0xfcbbff9e0
```
---

# Function Templates
Describes what the function is.
Can be used to generate many overloaded functions, each using different data types.

For example, say you have a max function that has 3 overloaded versions to accept different types.
```cpp
int max(int x, int y){
    return (x > y) ? x : y ;
}

double max(double x, double y){
    return (x > y) ? x : y ;
}

std::string max(std::string x, std::string y){
    return (x > y) ? x : y;
}
```
So we have 3 functions, and they all have the exact same functionality, the only difference is the typing, so in an instance such as this you can define and use the T operator, which will allow you to pass any type to the function!

Imagine T represents "thing" because we aren't really sure what the data type is!
```cpp
template <typename T, typename U>
auto max(T x, U y){
    return (x > y) ? x : y ;
}
```
---

# Objects & Classes
A collection of attributes, methods, and variables.
Examples are: Car, Player, Enemy, Phone, etc.
created from a class which is the objects "blueprint".

First lets define a class!
```cpp
#include <iostream>

class Player{
    public:
        //define the class variables
        std::string name;
        int level;
        int highscore;
        
        //define the class methods/functions
        void attack(){ std::cout << "Attack"; }
        void move(){ std::cout << "Walking"; }
}

int main(){

    //create new object of player class
    Player player1;

    //set the newly created objects data
    player1.name = "Skye";
    player1.level = 1;
    player1.highscore = 0;

    //optionally call the classes methods
    player1.attack(); //prints Attack
    player1.move(); //prints Walking

    return 0;
}
```
---

# Class Constructors
Here's how to make a constructor for a class.
```cpp
//define the new class, with its constructor
class Student {
    //define public variables
    public:
        std::string name;
        int age;
        double gpa;

    //define the constructor with the same name as the class/object
    Student(std::string name, int age, double gpa){
        this->name = name;
        this->age = age;
        this->gpa = gpa;
    }
};

//Example of instantiating the object with the constructor
int main() {
    Student student1("Spongebob", 27, 3.2);
    
    //the following console prints
    std::cout << student1.name; //Spongebob
    std::cout << student1.age;  //27
    std::cout << student1.gpa;  //3.2

    return 0;
}
```
---

# Overloaded Constructors
These are good for when you have items that have multiple possible constructors to choose from.
```cpp
class IceCream {
    public:
        std::string flavour1;
        std::string flavour2;
    
    //Constructor #0
    IceCream() { }

    //Constructor #1
    IceCream(std::string flavour1){
        this->flavour1 = flavour1;
    }
    
    //Constructor #2
    IceCream(std::string flavour1, std::string flavour2){
        this->flavour1 = flavour1;
        this->flavour2 = flavour2;
    }
}

int main(){
    
    IceCream icecream1("vanilla"); //chooses constructor #1 automagically
    IceCream icecream2("vanilla", "tiger"); //chooses constructor #2 automagically
    IceCream icecream3; //chooses constructor #0 automagically
    
    return 0;
}
```
---

# Abstraction & Getters/Setters
Imagine, you are coding a Stove, and someone hacks into it and changes all the public variables we declared up there, and sets the furnace to 100000 degrees to destroy everything. 🔥

That would suck.

So we should use private variables and use getters and setters for better protection over our variables.
And then use getters and setters that will allow these variables to be read / modified.
```cpp
#include <iostream>
#include <algorithm> //for std::max

class Stove {
    private:
        int temp = 210; //in celcius

    public:
        Stove(){} //Empty constructor for no default temp

        //create constructor that sets the private variable by default
        Stove(int temp){
            setTemp(temp);
        }

        //getter
        int getTemp(){ return temp; }

        //setter
        void setTemp(int temp){
            //validate the temp isnt being set too high
            int newTemp = std::max(300,temp);
            
            //validate the temp isnt being set in the negatives
            if (newTemp < 0) newTemp = 0;

            //update the temperature with the safely handled data
            this->temp = newTemp;
        }
};

int main(){
    Stove stove; //create an object of the Stove class
    stove.temp = 1000000; //throws error because we cant modify private variables directly
    std::cout << stove.getTemp(); //prints 210
    stove.setTemp(99999999); //try to set the temperature too high and destroy everything
    std::cout << stove.getTemp(); // prints 300 because we safely handled this a private variable

    Stove stove2(10);
    std::cout << stove2.getTemp(); //prints 10 

    return 0;
}
```
---

# Inheritence
A class inherit the attributes and methods of another class. Classes can be children of parent classes.
```cpp
//create parent class
class Animal {
    public:
        std::string name;
        int age;
        bool alive = true;

    void eat(){
        std::cout << "nom nom";
    }
};

//create child class that inherits the parent class, and add or override attributes/methods
class Dog : public Animal {
    void bark(){
        std::cout << "woof woof";
    }
};

int main(){
    Dog dog1;

    dog1.eat(); // nom nom
    dog1.bark(); // woof woof
    
    return 0;
}
```
---

# Headers
Classes, like shown above can get a little messy so for better organization of concerns we should instead use headers with our classes.
Let's use the above Animal class, and make a Header file for it.

First create a animal.h file for the header,
and animal.cpp for the class aka the implementation file.

Use #include "name" with quotes instead of brackets for self declared header include statements!

### Header File (The skeleton of the class)
```cpp
// animal.h 
#pragma once

class Animal {
    public:
        Animal(std::string name, int age, bool alive);
    void eat();

    std::string mName;
    int mAge:
    bool mAlive;
};
```
### Class File (The implementation file)
```cpp
// animal.cpp
#include "animal.h"

Animal::Animal(std::string name, int age, bool alive) {
    mName = name;
    mAge = age;
    mAlive = alive;
}

void Animal::eat(){
    std::cout << "nom nom";
}
```
### Main File
```cpp
// main.cpp
#include "animal.h"

int main(){
    Animal animal1{"Dog", 4, true};
    
    animal1.eat(); // nom nom

    return 0;
}
```
---

# Make a Class Console Printable 
### (Similar to overriding the toString method in c#)
```cpp
// rectangle.h
#pragma once
#include <iostream>

//define class skeleton
class Rectangle {
    public:
        Rectangle(int width, int height);
        int getWidth() const;
        int getHeight() const;
    private:
        int mWidth;
        int mHeight;
};
//set output stream, and use ref to rect
std::ostream& operator<<(std::ostream& os, const Rectangle& rect);
```

```cpp
// rectangle.cpp
#include "rectangle.h"

//define the constructor
Rectangle::Rectangle(int width, int height){
    mWidth = width;
    mHeight = height;
}

//get width
Rectangle::getWidth(){
    return mWidth;
}

//get height
Rectangle::getHeight(){
    return mHeight;
}

//class to console method
std::ostream& operator<<(std::ostream& os, const Rectangle& rect) {
   return  os << "Rect(w: " << rect.getWidth() << ", h: " << rect.getHeight() << ")";
}
```

```cpp
// main.cpp
#include <iostream>
#include <string>
#include "rectangle.h"

int main(){

    Rectangle rect{100,100};
    std::cout << rect; // will succesfully print itself in the console :)

    return 0;
}
```