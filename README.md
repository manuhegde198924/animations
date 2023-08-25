# animations
hosted link of project:https://manuhegde198924.github.io/animations/
steps of projects:https://github.com/manuhegde198924/animations/issues/1

“Animation” is a loose term, in web design usually referring to anything that involves movement.
CSS transitions are one tool we are given to manipulate elements on state changes or mouse events,
and when combines with transform, can resize, rotate, skew or flip elements to create a variety of interactions and effects.
There are two ways to animate web elements in CSS: the animation and transition properties. 
The animation property allows you to change the properties of an element over a specific duration,
while transition defines how an element changes over a specific duration.
Another new feature in CSS3 is the presence of transitions, transformations, and animations. These functions can replace the animated images, flash animations, and JavaScripts in the existing or new web pages. The difference between transitions, transforms, and animations isn't trivial. Animations are constructed with a range of @keyframes, where each @keyframes handles different states of your element in time. Transitions also describe the state of element between start and end. Transitions are mostly triggered by CSS changes, such as a mouse over (hover) of an element.

To make things clear, it is important to keep in mind the button that is about to be pressed. The button will have two states: pressed and not pressed. Without transitions and animations, we are enabled to style these states only. The color of the button is white, and its color becomes red when you hover the mouse over it. (In CSS terms, its state becomes hovered by adding the :hover pseudo class.) In this case, the transition describes how the hovered button becomes red. For example, the change in color from white to red in two seconds (which makes it pink halfway) shows that the start of the color change is slow and changes faster as time passes. Using animations here enables us to describe the state of the button for every time interval between the start and end. For example, you don't have to change the color from white to red, but the change covers all the states, from white, blue, green, and finally to red.

Transformations change the position of an element and how it looks. They do not depend on the state of the element. Some of the possible transformations are scaling, translating (moving), and rotating.

In practice, we use a combination of animations, transformations, and/or transitions in most situations. Also, in this case, vendor-specific rules will play an important role.

Now, a transformation will be added to our example.

Using the example code with rounded corners and gradients, copy the following code to less/transition.less or open less/transition.less and add the following code to the beginning of the file:

/* Mixin */
.transition (@prop: all, @time: 1s, @ease: linear) {
-webkit-transition: @prop @time @ease;
-moz-transition: @prop @time @ease;
-o-transition: @prop @time @ease;
-ms-transition: @prop @time @ease;
transition: @prop @time @ease;
}

This mixin has three variables; the first will be the property (@prop) that you will change. This can be height, background-color, visibility, and so on. The default value all shouldn't be used in the production code as this will have a negative effect on performance. @time sets the duration in milliseconds or seconds with s appended to it. The last variable, @ease, sets the transition-timing-function property. This function describes the value of a property, given that a certain percentage of it has been completed. The transition-timing-function property describes the completeness of the transition as a function of time. Setting it to linear shows the effect with the same speed from start to end, while ease starts slow and ends slow, having a higher speed in the middle. The predefined functions are ease, linear, ease-in, ease-out, ease-in-out, step-start, and step-end.

Now, you can edit less/transition.less to use this mixin. You can set the background color of the body when you hover over it. Note that you don't need to use the transition to change the gradient color but rather change the background-color attribute. You are using background-color because transition-duration doesn't have a visible effect on the gradient. The code of the background-color transition is as follows:

#content{
background-color: white;
min-height: 300px;
.roundedcornersmixin(20px);
.transition(background-color,5s);
}
#content:hover{
background-color: red;
}

If you renamed the Less file, for example, to less/transition.less, you would also have to change the reference in your HTML file to the following code:

 <link rel="stylesheet/less" type="text/css" href="less/transition.less" />

If you load the HTML file in the browser, you will be able to see the results in the browser. Move your mouse over the content and see it change from white to red in 5 seconds.

Finally, a second example that rotates the header can be added. In this example, you will use @keyframes. Using @keyframes will be complex. So, in this case, you can define some vendor-specific rules and add these animation properties to #header: as follows:

@-moz-keyframes spin { 100% { -moz-transform: rotate(360deg); } }
@-webkit-keyframes spin { 100% { -webkit-transform: rotate(360deg); } }
@keyframes spin { 100% { -webkit-transform: rotate(360deg); transform:rotate(360deg); } }
#header{
    -webkit-animation:spin 4s linear infinite;
    -moz-animation:spin 4s linear infinite;
    animation:spin 4s linear infinite;
}

You can add the preceding code to our example files or open less/keyframes.less.

If you renamed the Less file, for example, to less/keyframes.less, you also have to change the reference in your HTML file to the following code:

 <link rel="stylesheet/less" type="text/css" href="less/keyframes.less" />

Now, load the HTML file in the browser and watch your results. Amazing, isn't it? With a little bit of creative thinking, you will see the possibilities of creating a rotating windmill or a winking owl using only CSS3. However, the first thing that should be done is to explain the code used here in more detail. As mentioned earlier, there are many cases in which you would make combinations of animations and transformations. In this example, you also get to animate a transformation effect. To understand what is going on, the code can be split into three parts.

The first part is @keyframes, shown in the following code, which describe the value of the CSS properties (transformation in this case) as a function of the percentage of the animation completeness:

@keyframes spin { 100% { -webkit-transform: rotate(360deg); transform:rotate(360deg); } }

These keyframes have been given the name reference spin, which is not a special effect but only a chosen name. In the preceding example, a state of 100 percent completeness is described. At this state, the animated element should have made a rotation of 360 degrees.

This rotation is the second part that needs our attention. The transformation describes the position or dimensions of an element in the space. In this example, the position is described by the number of degrees of rotation around the axis, 360 degrees at 100 percent, 180 degrees at 50 percent, 90 degrees at 25 percent, and so on.

The third part is the animation itself, described by: animation:spin 4s linear infinite;. This is the shorthand notation of settings of the subproperties of the animation property. In fact, you can write this as the following code, without the vendor-specific rules:

animation-name: spin;
animation-duration: 4s;
animation-timing-function:linear;
animation-iteration-count:  infinite;

You can use these three parts to build a complete animation. After doing this, you can extend it. For example, add an extra keyframe, which makes the time curve nonlinear, as follows:

@keyframes spin {
50% { transform: rotate(10deg);}
100% {transform: rotate(360deg); }
 }

You can add a second property using background-color. Don't forget to remove the gradient to see its effect. This is shown in the following code:

@-moz-keyframes spin {
50% { transform: rotate(10deg); background-color:green;}
100% { transform: rotate(360deg); }
 }
//.gradient(red,yellow);
