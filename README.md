Download Link: https://assignmentchef.com/product/solved-cs2030s-practical-assessment-i-class-scheduling
<br>
<h3></h3>

<h4>Problem Description</h4>

Before the start of each semester, all University departments undergo a class scheduling exercise so that the timetable can be released early for students to plan their coursework.

We shall look at a scaled down version of such an exercise where classes are scheduled within a single day. A module comprise only two types of classes:

<ul>

 <li>Lecture — two hours per session</li>

 <li>Tutorial — one hour per session</li>

</ul>

A class can be represented as follows

<pre>CS2030 L1 @ LT19 [hchia] 10--12</pre>

which represents a <tt>CS2030</tt> (<tt>L</tt>)ecture with class-id <tt>L1</tt> at the venue <tt>LT19</tt>, and taught by <tt>hchia</tt> from <tt>10</tt>am to <tt>12</tt>nn.

A typical single-day schedule for one module could be

<pre>CS2030 L1 @ LT19 [hchia] 10--12CS2030 T1 @ SR7 [tsim] 12--13CS2030 T2 @ SR8 [hchia] 14--15CS2030 T3 @ SR7 [dlee] 15--16CS2030 T4 @ SR8 [ehan] 15--16CS2030 L2 @ LT19 [hchia] 16--18</pre>

Notice that tutorial classes of a module can be scheduled to run in parallel (such as tutorials <tt>T3</tt> and <tt>T4</tt>), provided that the venues and the module instructors are different. Moreover, since each lecture class serves all students in a module, <tt>L1</tt> and <tt>L2</tt> cannot clash. Not only that, a lecture of a module cannot clash with a tutorial of the same module. In other words, we do not split students of a module into different lecture groups, but they are split into different tutorial groups.

<h4>Task</h4>

Your task is to write a Java program to facilitate the creation of a single-day class schedule for a number of modules. Classes are scheduled one at a time only if they do not clash with other classes. Take note of the following:

<ul>

 <li>there are two types of classes: lecture (a class prefixed with <tt>L</tt>), and tutorial (a class prefixed with <tt>T</tt>)</li>

 <li>each class has a unique identifier represented by <tt>L</tt> or <tt>T</tt> followed by an integer class number: e.g. <tt>L1</tt>, <tt>T1</tt>, <tt>T2</tt>, etc…</li>

 <li>venues used for lectures will not be used for tutorials, and <em>vice versa</em></li>

</ul>

This task is divided into several levels. Read through all the levels to see how the different levels are related.

Remember to:

<ul>

 <li>write each class in a separate <tt>.java</tt> file</li>

 <li>always compile your program files first before using <tt>jshell</tt> to test your program</li>

 <li>declare object properties starting with <tt>private final</tt>…</li>

 <li>you may import any Java package; however do not use the wild card <tt>*</tt> in your import statements, else CodeCrunch will render your program uncompilable</li>

 <li>all tests use valid arguments; you need not check for validity of arguments; <tt>null</tt> will not used for the tests</li>

</ul>

<table border="1" cellpadding="10">

 <tbody>

  <tr>

   <td><h4>Level 1</h4>Write a Java class <tt>Instructor</tt> to facilitate the creation of <strong>immutable</strong> objects to represent the instructors. Include the overriding <tt>equals</tt> method to compare if two instructor objects are the same.<pre>$ javac your_java_files$ jshell -q your_java_files_in_bottom-up_dependency_order &lt; test1.jshjshell&gt; new Instructor("hchia")$.. ==&gt; hchiajshell&gt; new Instructor("hchia").equals(new Instructor("tsim"))$.. ==&gt; falsejshell&gt; new Instructor("tsim").equals(new Instructor("tsim"))$.. ==&gt; truejshell&gt; new Instructor("tsim").equals((Object)(new Instructor("tsim")))$.. ==&gt; truejshell&gt; new Instructor("hchia").equals("hchia")$.. ==&gt; falsejshell&gt; /exit</pre></td>

  </tr>

  <tr>

   <td><h4>Level 2</h4>Write appropriate Java classes to facilitate the creation of an <strong>immutable</strong> object to represent a scheduled class. Each class (<tt>Lecture</tt> or <tt>Tutorial</tt>) is defined by the following:

    <ul>

     <li>module code represented as a <tt>String</tt></li>

     <li>class-id represented by a positive integer</li>

     <li>venue-id represented as a <tt>String</tt></li>

     <li>start time represented as an integer in the range <tt>[8, 23]</tt></li>

     <li>duration of <tt>2</tt> hours for lecture, and <tt>1</tt> hour for tutorial</li>

     <li>the module instructor of the class</li>

    </ul>You will also need to include the methods <tt>hasSameModule</tt>, <tt>hasSameInstructor</tt> and <tt>hasSameVenue</tt>, that can be called via any class (<tt>Lecture</tt> or <tt>Tutorial</tt>) and takes in another class as argument.<pre>$ javac your_java_files$ jshell -q your_java_files_in_bottom-up_dependency_order &lt; test2.jshjshell&gt; Lecture l1 = new Lecture("CS2030", 1, "LT19", new Instructor("hchia"), 10)jshell&gt; Tutorial t1 = new Tutorial("CS2030", 1, "SR7", new Instructor("tsim"), 12)jshell&gt; Tutorial t2 = new Tutorial("CS2030", 2, "SR8", new Instructor("hchia"), 12)jshell&gt; Lecture l2 = new Lecture("CS2040", 1, "LT19", new Instructor("tanst"), 12)jshell&gt; l1.hasSameModule(t1)$.. ==&gt; truejshell&gt; l1.hasSameModule(l2)$.. ==&gt; falsejshell&gt; l1.hasSameInstructor(t1)$.. ==&gt; falsejshell&gt; l1.hasSameInstructor(t2)$.. ==&gt; truejshell&gt; l1.hasSameVenue(l2)$.. ==&gt; truejshell&gt; t1.hasSameVenue(t2)$.. ==&gt; falsejshell&gt; /exit</pre></td>

  </tr>

  <tr>

   <td><h4>Level 3</h4>Define the <tt>clashWith</tt> method that determines if two scheduled classes clash. Recall that no two lecture classes can have overlapping time slots. However tutorials of the same module can be scheduled in parallel if the instructors and venues are different.<pre>$ javac your_java_files$ jshell -q your_java_files_in_bottom-up_dependency_order &lt; test3.jshjshell&gt; Lecture hchia_L = new Lecture("CS2030", 1, "LT19", new Instructor("hchia"), 10)jshell&gt; hchia_L.clashWith(hchia_L)$.. ==&gt; truejshell&gt; hchia_L.clashWith(new Lecture("CS2030", 1, "LT19", new Instructor("hchia"), 10))$.. ==&gt; truejshell&gt; hchia_L.clashWith(new Lecture("CS2030", 1, "LT19", new Instructor("tsim"), 11))$.. ==&gt; truejshell&gt; hchia_L.clashWith(new Lecture("CS2030", 1, "LT19", new Instructor("hchia"), 12))$.. ==&gt; falsejshell&gt; hchia_L.clashWith(new Lecture("CS2040", 1, "LT19", new Instructor("tanst"), 10))$.. ==&gt; truejshell&gt; Tutorial tsim_T = new Tutorial("CS2030", 1, "SR7", new Instructor("tsim"), 10)jshell&gt; tsim_T.clashWith(tsim_T)$.. ==&gt; truejshell&gt; tsim_T.clashWith(hchia_L)$.. ==&gt; truejshell&gt; hchia_L.clashWith(tsim_T)$.. ==&gt; truejshell&gt; tsim_T.clashWith(new Tutorial("CS2030", 2, "SR8", new Instructor("ehan"), 10))$.. ==&gt; falsejshell&gt; tsim_T.clashWith(new Tutorial("CS2030", 2, "SR7", new Instructor("ehan"), 10))$.. ==&gt; truejshell&gt; tsim_T.clashWith(new Tutorial("CS2030", 2, "SR8", new Instructor("tsim"), 10))$.. ==&gt; truejshell&gt; tsim_T.clashWith(new Tutorial("CS2040", 2, "SR8", new Instructor("tsim"), 10))$.. ==&gt; truejshell&gt; /exit</pre></td>

  </tr>

  <tr>

   <td><h4>Level 4</h4>Write a Java class <tt>Schedule</tt> to create an <strong>immutable</strong> schedule of classes. Include a method <tt>add</tt> that takes in a class as argument and adds to the current schedule only if the class does not clash with existing classes in the schedule.<pre>$ javac your_java_files$ jshell -q your_java_files_in_bottom-up_dependency_order &lt; test4.jshjshell&gt; Schedule s0 = new Schedule()jshell&gt; s0 = s0.add(new Lecture("CS2030", 1, "LT19", new Instructor("hchia"), 10))jshell&gt; System.out.println(s0)CS2030 L1 @ LT19 [hchia] 10--12jshell&gt; Schedule s = s0.add(new Tutorial("CS2030", 1, "SR7", new Instructor("tsim"), 11))jshell&gt; System.out.println(s)CS2030 L1 @ LT19 [hchia] 10--12jshell&gt; s = s.add(new Tutorial("CS2030", 1, "SR7", new Instructor("tsim"), 12))jshell&gt; System.out.println(s)CS2030 L1 @ LT19 [hchia] 10--12CS2030 T1 @ SR7 [tsim] 12--13jshell&gt; System.out.println(s0)CS2030 L1 @ LT19 [hchia] 10--12jshell&gt; s = s.add(new Lecture("CS2030", 2, "LT19", new Instructor("hchia"), 16))jshell&gt; s = s.add(new Lecture("CS2040", 1, "I3-AUD", new Instructor("tanst"), 15))jshell&gt; s = s.add(new Tutorial("CS2030", 4, "SR8", new Instructor("ehan"), 15))jshell&gt; s = s.add(new Tutorial("CS2030", 3, "SR7", new Instructor("dlee"), 15))jshell&gt; s = s.add(new Tutorial("CS2030", 2, "SR7", new Instructor("hchia"), 14))jshell&gt; System.out.println(s)CS2030 L1 @ LT19 [hchia] 10--12CS2030 T1 @ SR7 [tsim] 12--13CS2030 T2 @ SR7 [hchia] 14--15CS2030 T3 @ SR7 [dlee] 15--16CS2030 T4 @ SR8 [ehan] 15--16CS2040 L1 @ I3-AUD [tanst] 15--17CS2030 L2 @ LT19 [hchia] 16--18jshell&gt; /exit</pre>Note that the output of a schedule is in chronological order of start time. In the case of two classes have the same start time, then the earlier module should come first. If the module codes are also the same, then the smaller class-id should come first. Moreover, do not worry about extra blank lines in your output, all blank lines will be ignored in CodeCrunch.<em>Hint: Java’s <tt>List</tt> interface provides a sort method.</em></td>

  </tr>

  <tr>

   <td><h4>Bonus Level 5 [No marks awarded]</h4>Congratulations if you have made it thus far! Proceed on to this level to gain a priceless sense of personal achievement!As you can see, the clash of classes imposes a constraint on when a class can be scheduled. Other than such <em>hard constraints</em>, there are also <em>soft constraints</em> which may affect timetabling. Two examples of such constraints are:

    <ol>

     <li>Instructor hchia’s lunch time is from 2 to 4pm</li>

     <li>Venues used for lectures must be scheduled with at least a one hour gap between them for disinfecting purposes (<em>again due to COVID..</em>)</li>

    </ol>Individual constraints are defined in separate Java classes. Each constraint makes use of a <tt>test</tt> method that takes in a schedule and applies the constraint check. The <tt>test</tt> method returns <tt>true</tt> if the constraint is met, or <tt>false</tt> otherwise.Your task is to define Java classes <tt>HchiaLunch</tt> and <tt>GapBetweenLectures</tt> for constraints (1) and (2) above.  You may only import <tt>Iterator</tt> from <tt>java.util</tt>.<pre>$ javac your_java_files$ jshell -q your_java_files_in_bottom-up_dependency_order &lt; test5.jshjshell&gt; Schedule s = new Schedule().   ...&gt; add(new Lecture("CS2030", 1, "LT19", new Instructor("hchia"), 10)).   ...&gt; add(new Tutorial("CS2030", 1, "SR7", new Instructor("tsim"), 12)).   ...&gt; add(new Lecture("CS2030", 2, "LT19", new Instructor("hchia"), 16)).   ...&gt; add(new Lecture("CS2040", 1, "I3-AUD", new Instructor("tanst"), 15)).   ...&gt; add(new Tutorial("CS2030", 4, "SR8", new Instructor("ehan"), 15)).   ...&gt; add(new Tutorial("CS2030", 3, "SR7", new Instructor("dlee"), 15)).   ...&gt; add(new Tutorial("CS2030", 2, "SR7", new Instructor("hchia"), 14))jshell&gt; System.out.println(s)CS2030 L1 @ LT19 [hchia] 10--12CS2030 T1 @ SR7 [tsim] 12--13CS2030 T2 @ SR7 [hchia] 14--15CS2030 T3 @ SR7 [dlee] 15--16CS2030 T4 @ SR8 [ehan] 15--16CS2040 L1 @ I3-AUD [tanst] 15--17CS2030 L2 @ LT19 [hchia] 16--18jshell&gt; List constraints = List.of(new HchiaLunch(), new GapBetweenLectures());jshell&gt; List results = new ArrayList&lt;&gt;();jshell&gt; for (Constraint c : constraints) {   ...&gt;     results.add(c.test(s));   ...&gt; }jshell&gt; resultsresults ==&gt; [false, true]jshell&gt; /exit</pre>From the above sample run, the <tt>HchiaLunch</tt> constraint is not met as he has a tutorial class from 2 to 3pm. However, the <tt>GapBetweenLectures</tt> is met as the two lectures at <tt>LT19</tt> is four hours apart; only one lecture is scheduled at <tt>I3-AUD</tt>.<em>Design Tips:</em>Suppose the <tt>Schedule</tt> class is implemented with the following list attribute:<pre>class Schedule {    private final List list... // use of raw type to mask out implementation details    ...}</pre>Every soft-constraint check would entail going through the list of classes. While an accessor (getter) method can be written within <tt>Schedule</tt> to return the list to the constraint checker, this inevitably exposes the internal implementation details.The proper design is to make <tt>Schedule</tt> an <tt>Iterable</tt>. The following Jshell session demonstrates how we can iterate over an <tt>Iterable</tt>.<pre>jshell&gt; class A implements Iterable {   ...&gt; privatejshell&gt; class A implements Iterable {   ...&gt; private final List list = List.of("abc", "xyz");   ...&gt; @Override   ...&gt; public Iterator iterator() {   ...&gt; return this.list.iterator();   ...&gt; }}|  created class Ajshell&gt; for (String s : new A()) {   ...&gt; System.out.println(s);   ...&gt; }abcxyz</pre></td>

  </tr>

 </tbody>

</table>