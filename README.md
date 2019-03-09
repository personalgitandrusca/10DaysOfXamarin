By now you should have your environment setup and ready to start creating your first Xamarin application. If you don't yet, make sure you check out Day 0 first.

# Create your first Xamarin app

So let's start by creating our first Xamarin app. The process is slightly different depending on the Operating System that you are currently using. So check the corresponding video below to follow the steps to create the project on macOS or Windows.

[https://www.youtube.com/watch?v=a2voTRVe4Es](https://www.youtube.com/watch?v=a2voTRVe4Es)

[https://www.youtube.com/watch?v=wZOhxb5pvUw](https://www.youtube.com/watch?v=wZOhxb5pvUw)

# Challenge

Now that you know how to create an app, here is your challenge:

## Problem

Create an app that requests the user's name through an Entry and, on the click of a button, displays -on a label- a greeting to that user.

Display an alert if the user clicks the button, but there is nothing written on the entry.

## App description

The app's interface should contain three elements:

- The Entry for the user's name
- A Label that will display the greeting
- A button that the user will have to click to display the greeting.

The app should then react to the click of the button, get the value that is written on the entry, and display it in this format: "Hello {User_Name}, welcome to 10 Days of Xamarin".

## Constraints

If the Entry has no text, the label should not change. Instead, the app should display an alert to the user letting them know that their name is required.

# Solution

Your project before implementing this solution:

[Initial source code](/LaloCo/10DaysOfXamarin/tree/Day1/initial)

## Defining the Interface

XAML is the language that you will use to create the shared interfaces. As mentioned before, this will later be translated into entirely native elements, depending on which platform your app is running.

Defining these three elements will be quite straight forward, but you do need to make sure that you add them inside a container. The go-to container for "forms" is a StackLayout. This container will, as its name suggests, stack all of the elements together. This way they are displayed correctly, and not on top of each other — this way they are displayed correctly, and not on top of each other.

Some templates will already contain a StackLayout, so change the Label that is there by default for the three required elements:

    <StackLayout Margin="16,20,16,0">
        <Entry Placeholder="Enter your name"/>
        <Button Text="Say hello"/>
        <Label Text="Hello stranger, welcome to 10 Days of Xamarin."
               FontSize="20"/>
    </StackLayout>

This definition will be enough for you to see on the designer (included on Visual Studio) how your app will look when running.

[https://www.youtube.com/watch?v=Q9KOpY4zCoo](https://www.youtube.com/watch?v=Q9KOpY4zCoo)

[https://www.youtube.com/watch?v=ATmbD_8OfP8](https://www.youtube.com/watch?v=ATmbD_8OfP8)

Do notice that I added some margin to the container. If you didn't add this margin, all the elements inside the container would be displayed all the way to the sides, and wouldn't look very good. Alternatively, you could also add the margin to each element; adding it to the container, however, means that you only need to add it once.

I also set a placeholder for the entry, so users know what they are supposed to write, as well as the text for the button. The label is displaying a default text and has a font size set to 20, which is bigger than the default one. You can experiment with this number to make the label look the way you want it.

## Handling the click of a button

Handling the click of a button requires a couple of steps to be completed. The first one is to set the event handler for the Click event of the button. I usually do this from XAML, but you could also do this from C#. The second step is to define that event handler, which I will create as a method. Notice though that Intellisense helps you with this second step as soon as you complete the first:

[](https://www.notion.so/1992a315899c40d3ae6966b45dfe86ed#ad6c7b69795e43f3b2715d6bf1bcca73)

[](https://www.notion.so/1992a315899c40d3ae6966b45dfe86ed#2d24a61e9b4446fc8ed770c7b2071a20)

So your button now looks like this:

    <Button Clicked="Handle_Clicked"
            Text="Say hello"/>

So you now have a new method over in the C# file for this same Page: the event handler for the click of the button. This method is where you will create the functionality. Now before we jump over to that file, there is one final thing we need to do in the XAML file. It turns out that, if we want to be able to access the defined elements from C# (which we will need to do since we need the text in the entry and to change the label's text) they need to have a name.

We don't need to name the button, because we won't need to get or set any of its properties from the code behind, but the other two elements will need to set the Name property:

    <Entry x:Name="nameEntry"
           Placeholder="Enter your name"/>
    <Button Clicked="Handle_Clicked"
            Text="Say hello"/>
    <Label x:Name="greetingLabel"
           Text="Hello stranger, welcome to 10 Days of Xamarin."
           FontSize="20"/>

Notice the naming convention. Ours is a simple-enough interface, but as your interfaces grow more complicated, the naming convention becomes more and more critical, which is why you should always try to use a naming convention that helps you quickly identify elements from each other. Here, for example, I not only identify each element with its basic functionality (name and greeting) but by its type also (entry and label). Feel free to use this same naming convention or another that you may find useful.

## Coding the functionality

All that is left for us to do is display the greeting then. A couple of things are required here. First, we need to get the value that is written in the entry, and second, we need to set the text for the label.

You should also not forget to check if the entry has text in it, and display an error message if it doesn't.

    void Handle_Clicked(object sender, System.EventArgs e)
    {
        if(!string.IsNullOrWhiteSpace(nameEntry.Text))
        {
            greetingLabel.Text = $"Hello {nameEntry.Text}, welcome to 10 Days of Xamarin.";
        }
        else
        {
            DisplayAlert("Error", "Your name can't be empty", "Oh right");
        }
    }

If you were to test your app now, you should see something like this:

[](https://www.notion.so/1992a315899c40d3ae6966b45dfe86ed#0afd32fe6011410590e00068c1a7f9c6)

[](https://www.notion.so/1992a315899c40d3ae6966b45dfe86ed#a2ba254d0d23464fa2e5679fa86c52bf)

[](https://www.notion.so/1992a315899c40d3ae6966b45dfe86ed#006919c297a84d6b8990a5a3c8ee6431)

Of course, the result will be identical (but rendered natively) on Android:

[](https://www.notion.so/1992a315899c40d3ae6966b45dfe86ed#6cd45006e584475f871e72795d4ff3be)

[](https://www.notion.so/1992a315899c40d3ae6966b45dfe86ed#ee48354436734c189d2d48e6685ea5f3)

[](https://www.notion.so/1992a315899c40d3ae6966b45dfe86ed#4ecfdc3ea0c94c38b9b526bc2698181c)

So there you have it, your Day 1 challenge is now complete.

[Check final source code](/LaloCo/10DaysOfXamarin/tree/Day1/final)

# Learn more

Want your app to look ok on an iPhone X -or Xr, or Xs, or Xs Max-? Because if you test this on one of those devices, the notch will get on the way.

[Correctly Display Your App on iPhones with a Notch](https://lalorosas.com/blog/adapting-to-the-notch)