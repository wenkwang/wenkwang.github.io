---
layout: post
title: C#.NET - Delegates
---
In C#, the delegate is a topic not very straightforward to understand, especially for those who are mainly playing in the Java world like me. Recently, I got a chance to look over some materials about delegates in C# and I'd like to write it down here for my record and hopefully help you guys as well.  
From what I can see at this point, delegates have two main interesting features. One is encapsulation, the other is composition. But before I go deeper with these two features, let me describe some basic concepts first.

**What is the delegate?**  
The delegate is very similar to the method pointer in C++, but unlike the pointers, delegates are object-oriented, type safe and secure. According to the official document, the definition of the delegate is:
A delegate is a type that represents references to methods with a particular parameter list and return type.

**What is the delegate used for?**  
Delegates are used to pass methods as an argument into other methods. Just like you pass other types of parameter into methods, such as int, char, string, the delegate is the type for methods, so you can declare within a certain method to pass in a delegate type of parameter as the argument.

**How to declare a delegate?**  
A delegate class is derived from System.Delegate, the return type and parameters define what kind of methods could be associated with the instance of this type. Here is an example:
public delegate int processDelegate(int a, int b);
In this example, I declare a delegate type, and this type defines the methods should have two int parameters and their return type should be int.

**Encapsulation**  
Encapsulation is a very common concept in the programming world. Here for the delegate, it mainly means to separate the specification and implementation of the delegate type parameter. The method caller doesn't need to know the details about how the method will do, it only needs to know what type of method should be used here.

For example:

```c#
namespace MusicPlayer
{
    public delegate void PlayMusicDelegate(ArrayList songlist);
    public class Player
    {
        ArrayList songList = new ArrayList();
        public void InitializeSongs(ArrayList list)
        {
            ...
        }
        public void PlayMusic(PlayMusicDelegate play)
        {
            play(songList);
        }
    }
    public class Mode
    {
        public void PlayGuitar(ArrayList list)
        {
            ...
        }
        public void PlayKeyboard(ArrayList list)
        {
            ...
        }
    }
}
namespace PlayerClient
{
    using MusicPlayer;
    class Test
    {
        static void main()
        {
            Player player = new Player();
            Mode mode = new Mode();
            ArrayList list = new ArrayList();
            player.InitializeSongs(list);
            player.PlayMusic(new PlayMusicDelegate(mode.PlayGuitar));
            player.PlayMusic(new PlayMusicDelegate(mode.PlayKeyboard));
            return;
        }
    }
}
```
In this example above, the method PlayMusic in class Player doesn't need to know which exact the method is passed in, it only cares the type of the method, its return type and parameters. On more thing here is that the delegate objects are immutable, once a delegate is created with a certain method, then it won't change. If you want to associate with another method, you need to create a new delegate object.

**Composition**
This is the most interesting part I found about the delegate. For delegate objects, they could be composed with '+' operator, and once you call the composed objects, all the delegate components will be invoked. Of course, all these delegate objects should be in the same type. Also, you can use '-' operator to remove a certain delegate from a composed object.

Here is an example:

```c#
public delegate void PlayMucisDelegate(Song song);
public static void Guitar(Song song)
{
    ...
}
public static void Keyboard(Song song)
{
    ...
}
public class Player
{
    static void main()
    {
        Song song = new Song();
        PlayMusicDelegate a, b, c, d;
        a = new PlayMusicDelegate(Guitar);
        b = new PlayMusicDelegate(Keyboard);
        c = a + b;
        d = c - a;
        c(song);
        d(song);
        return;
    }
}
```

In the example above, calling the delegate c will invoke the method Guitar first, then keyboard, calling the delegate d will invoke the method Keyboard. This logic is pretty straightforward and this feature is a good fit to be used in listeners.
There are some other details about the delegate, such as the relationship between the delegate and event, the comparison between the delegate and interface. You can check out the links below for further information.

**References:**  
[Delegates Tutorial](https://msdn.microsoft.com/en-us/library/aa288459(v=vs.71).aspx)  
[C# Programming Guide - Delegates](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/delegates/)