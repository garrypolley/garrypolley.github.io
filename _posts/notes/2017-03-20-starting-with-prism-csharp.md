---
layout: post
title: 'Windows Desktop App: Prism Default Page'
---

This will be short because it's mostly a note to myself. I just got started doing `WPF` applications using, [Prism](https://github.com/PrismLibrary/Prism).

The most useful part I've used so far has been this video: https://www.youtube.com/watch?v=ZfBy2nfykqY

What I what to cover specifically in this post: handling the default view/window of an applicaiton. If you followed the video
from the link posted above, you'll have an application that can do navigation and how data from other Views with a backed ViewModel.
The issue currently is a required click to start the first view. I've found a way to get a "default" view in place from this 
stackoverflow post: http://stackoverflow.com/a/39547006/1686511

Here is the code from stackoverflow:

```xml
<UserControl
             xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
             xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
             xmlns:prism="http://prismlibrary.com/"
             xmlns:i="http://schemas.microsoft.com/expression/2010/interactivity"
             xmlns:vm="clr-namespace:PrismTest.ViewModels"
             xmlns:view="clr-namespace:PrismTest.Views"
             x:Class="PrismTest.Views.TestView"
             prism:ViewModelLocator.AutoWireViewModel="True">
    <i:Interaction.Triggers>
        <i:EventTrigger EventName="Loaded">
            <i:InvokeCommandAction Command="{Binding LoadedCommand}" CommandParameter="{Binding Message, RelativeSource={RelativeSource FindAncestor, AncestorType={x:Type view:TestView}}}" />
        </i:EventTrigger>
    </i:Interaction.Triggers>
    <Grid>
        <StackPanel>
            <TextBlock Text="{Binding Message, RelativeSource={RelativeSource FindAncestor, AncestorType={x:Type view:TestView}}}"/>
            <TextBlock Text="{Binding Message}"/>
        </StackPanel>
    </Grid>
</UserControl> 
```


The most important part here is the use of the `i:Interaction` part. It allows you to call your navigation command from that trigger. 
So the code I've used in my application to default to the login view is: 

```xml
<i:Interaction.Triggers>
    <i:EventTrigger EventName="Loaded">
        <i:InvokeCommandAction Command="{Binding NavigateCommand}" CommandParameter="Login"></i:InvokeCommandAction>
    </i:EventTrigger>
</i:Interaction.Triggers>
```

With that I've been able to get the default login View and ViewModel to load and start handling the application. 
