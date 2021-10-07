# Talk: How to learn Rust

I wanted to write this short blog post to reflect on Tim McNamara's talk on the Rust youtube channel (watch it [here](https://www.youtube.com/watch?v=sDtQaO5_SOw)). In particular, I'll briefly consider:

- what I took from the talk.
- how I am trying to implement some of these ideas.
- what I still need to do.

## Outline of advice from the talk

Some general advice I want to consider:
- Start small, grow gradually: e.g. work with examples that give immediate feedback; gradually extend examples.
- Set effective motivations: *why am I learning Rust?*
- Create an effective environment: involves regular practice, find trusted people to ask questions, share through blog posts (*why i'm writing this today...*)

Some Rust specific advice for beginners to focus on:
- Traits and safe access to data.
- Form a foundation from the core of the language: structs, vectors, iteration, Result and Option.

## My Rust journey so far

Before starting to learn Rust, Python was the only language I knew so there are a lot of new concepts that I've been working through. Currently I'm working my way through [the book](https://doc.rust-lang.org/book/) and [Rust by example](https://doc.rust-lang.org/stable/rust-by-example/). With respect to concepts from the talk, here's a quick look into my Rust journey so far:
- When comibned, these learning resources start small and gradually extend examples. Rust by Example extends concepts encountered in *the book* and also provides some activities which have been fun/challenging. 
- Primary motivations:	genuine curiousity to learn another language (Python also self-taught); Rust might be helpful at some point during my PhD; Want to use [dapptools-rs](https://github.com/gakonst/dapptools-rs) for Solidity smart contract developments.
- Still need to wrap my head around *safe access to data* - maybe I need to see what **unsafe** access to data looks like?
- I have just started to look at traits and generics, though their usefulness quickly became obvious to me through examples.

## Learning about generics from the Rust Book
To round off this blog post, I'll write a few things I've learnt about generics in the past 24 hours. Generics enable behaviour to be expressed without knowing what will be there at compile time. This can avoid code duplication in situations where multiple structs or enums differ only be the type of values held.

Code for finding the largest value in a slice without using generics:

    fn largest_i32(list: &[i32]) -> i32 {
        let mut largest = list[0];
        
        for &item in list {
            if item > largest {
                largest = item;
            }
        }
        
        largest
    }
    
    fn largest_char(list: &[char]) -> char {
        let mut largest = list[0];
        
        for &item in list {
            if item > largest {
                largest = item;
            }
        }
        
        largest
    }
    
    fn main() {
        let number_list = vec![34, 50, 25, 100, 65];
        let result = largest_i32(&number_list);
        println!("The largest number is {}", result);
        
        let char_list = vec!['y', 'm', 'a', 'q'];
        let result = largest_char(&char_list);
        println!("The largest char is {}", result);
    }

Both `largest_i32` and `largest_char` share the same code in their function bodies. Using generics, this code can be rewritten as follows:

    fn largest<T>(list: &[T]) -> T {
        let mut largest = list[0];
        
        for &item in list {
            if item > largest {
                largest = item;
            }
        }
        
        largest
    }
    
    fn main() {
        let number_list = vec![34, 50, 25, 100, 65];
        let result = largest(&number_list);
        println!("The largest number is {}", result);
        
        let char_list = vec!['y', 'm', 'a', 'q'];
        let result = largest(&char_list);
        println!("The largest char is {}", result);
    }

Now, we only have one function `largest` that achieves the same result.
    
    


