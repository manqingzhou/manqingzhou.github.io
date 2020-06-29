---
title: Buffer Overflow
subtitle: System Call and Countermeasures
layout: post
---
By exploiting the operating systems, attackers can execute commands, potentially taking over the victim machines. One of the attack I have done is to gain the root privileage.

The vulnerabilities are based on an attacker sending more data to a vulnerable program than the original reserved input space all caused by sloopy programming not check the size of user input before moving it to memory. Here, I am gonna talk about the one that I did and am familar with: stack-based buffer overflow attack. 

To understand how it works, you should understand how a computer runs a program.When running a program, CPU feteches instructions from memory, one by one, in sequence. The CPU contains a very special register called the Instruction Pointer, which tells it where to grad the next instruction (pointer tells you the address of the instruction and then fetch).
<img src="/img/posts/prgram.png" alt="how a program run" align="center"/>

In one word, if you know where to place your malicious code, you can redirect the flow of execution.

Last thing we need to keep in mind is how a higher level language execute their command, this picture shows everything:
<img src="/img/posts/c_code.png" alt="how a program run" align="center"/>

And as you know if studied data structure before, stack is a data structure that store important information for each process running on a computer and follow tthe rule of Last-In, First-Out(LIFO). Similarly, when the computer puts data onto its stack, it pushed data element after data elements. Here, I dont want to touch on reture address, buffer and function calls, all you need to remember is `overflow`.

Some very vulnerabe C code
~~~
void sample_fuction()
{ char bufferA[50];
char bufferB[16];
printf("where do you live\n")
gets(bufferA);
strcpy(bufferA,bufferB);
return;
}
main()
{
sample_fuction()
printf("all done\n");
}
~~~
We got a couple of problems here, `gets` library puts no limitations on the amount of data and the `strcpy`? The attacker can simply overflow bufferB by simply typing between 17 and 50 characters in bufferA.

Imagine we just input bunch of 'A'. The return pointer on the stack would be filled with As. It tries to fetch the next instruction from a memory location that is the binary equivalent of a bunch of As (that would be hexadecimal 0x41414141 ... you can look it up!) And, there is higher chance we would get a nasty segmentation fault.

 
