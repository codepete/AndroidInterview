# Android Interview Dry-Run

## Question 1 - What’s your favorite tool or library for Android? Why is it so useful?
Dagger has to be one of my top libraries for Android. Dagger is a dependency injection library that automates instantiation or creation of objects that you use throughout your Android project. You define how to create your dependencies once and "inject" and reuse these dependencies anywhere. This removes a significant amount of boilerplate code and encourages abstraction, which makes for cleaner and more testable code. Through the use of a dependency graph it builds your dependencies in the correct order and with the correct components every time. This allows developers to focus on how to use an dependencies to build great features instead of focusing on how to create them. The learning curve is extremely high, but the benefits make it well worth the effort.

## Question 2 - You want to open a map app from an app that you’re building. The address, city, state, and ZIP code are provided by the user. What steps are involved in sending that data to a map app?
Intents and URI schemes are the two main components to achieve this. Android allows all apps to create their own URI scheme that enables third-party apps to utilize certain features that they've defined. For our particular scenario, Google Maps has provided a "geo" URI scheme with some predefined supported paths and parameters to achieve this - "geo:0,0?q=<user address>" is what we're looking for. After identifying the correct URI scheme and pattern we combine them like so:
1. Take your address information and build a String with each address component - separate by spaces. Uri encode this string.
2. Create a Uri object with "geo:0,0?q=<uri encoded string>". 
3. Create an Intent object with the ACTION_VIEW action and pass the Uri object you created in the previous step.
4. Set the package to Google Maps; however, its important to verify if the package exists
4. Call startActivity or startActivityForResult with the Intent that you created. 

## Question 3 - Implement a method to perform basic string compression using the counts of repeated characters. For example, the string aabcccccaaa would become a2b1c5a3. If the "compressed" string would not become smaller than the original string, your method should return the original string. The method signature is: “public static String compress(String input)” You must write all code in proper Java, and please include import statements for any libraries you use.
```java
public static String compress(String input) {
    if (input == null || input.isEmpty()) {
        return null;
    }

    StringBuilder builder = new StringBuilder();

    char currentVal = input.charAt(0);
    int count = 1;
    for (int i = 1; i < input.length(); i++) {
        char val = input.charAt(i);

        if (val == currentVal) {
            count++;
            continue;
        }

        builder.append(currentVal);
        builder.append(count);

        // Reset
        count = 1;
        currentVal = val;
    }

    builder.append(currentVal);
    builder.append(count);

    return builder.toString();
}
```

## Question 4 - List and explain the differences between four different options you have for saving data while making an Android app. Pick one, and explain (without code) how you would implement it.
1. SharedPreferences - For simple and small data objects like strings, numbers, and boolean values, SharedPreferences can be extremely useful and accessible from anywhere within your app as long as you have access to a Context object. Data stored in SharedPreferences can be used by other applications or made private. SharedPreferences is a key-value storage system like HashTables.
2. Device Storage (Internal & External) - You can use the mobile devices internal and external (SD) storage to store large files.
3. Sqlite Database - Great for storing large amounts of structured data. When the data you need to store moves beyond simple data types this is perfect for usage.
4. Network - Some apps opt to not store data on the device and instead store the data on their own servers through API calls. 

SharedPreferences is extremely easy to use. Use PreferenceManager to retrieve an instance of a SharedPreference by calling something like getDefaultSharedPreferences. With the SharedPreference object you then call edit() - this will provide you with a Editor instance. The Editor object can then store/map values by key using methods such as putString or putInt. Once you are done you can call commit() on the Editor object and your data will be persisted. 

## Question 5 - What are your thoughts about Fragments? Do you like or hate them? Why?
I think that for many developers Square, the payment company, pops into their minds when fragments are mentioned. Square set the community abuzz in 2014 when they released an article advocating against the usage of fragments and pushed for the usage of custom views. I personally believe fragments are great for having UI modularity in your code. I love that you are able to compose a single screen with multiple fragments. It is especially helpful in constructing master-detail views while supporting tablet - i.e. two-pane views for tablet and single pane view for phones. While I believe that the Square article is accurate in pointing out how complex fragment lifecycles are, I don't believe that there are any better alternatives out there. Custom views are good, but it becomes infinitely more complex when you don't have things like backstack management that fragments provide out of the box.

## Question 6 - If you were to start your Android position today, what would be your goals a year from now?
My goals a year from today would be:
- Be intimately acquainted with the codebase
- Contributing greatly to stability of the app and adding integral features
- Be able to be someone who can be counted on for everything related to the app
- Be able to mentor and help onboard newcomers
