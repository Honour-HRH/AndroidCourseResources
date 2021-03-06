# Android Programming: The Big Nerd Ranch Guide - Errata


## Chapter 1: Your First Android Application

### Page 26 
In the 2nd to last line the URL for the developer site link has an extra "http://" at the front. 

## Chapter 2: Android and Model-View-Controller

### Page 37

Button specification in the XML diagram shows `android:text="@string/next_question_button"`, but it should read `android:text="@string/next_button"`.

### Page 39 - Listing 2.6

Missing comma when creating the array:

    private TrueFalse[] mQuestionBank = new TrueFalse[] {
        new TrueFalse(R.string.question_oceans, true),
        new TrueFalse(R.string.question_mideast, false),
        new TrueFalse(R.string.question_africa, false) <-- comma needed at end of this line
        new TrueFalse(R.string.question_americas, true),
        new TrueFalse(R.string.question_asia, true), <-- extra trailing comma has no effect
    };
    
The extra trailing comma is not required, but we typically include it because it makes adding new items later easier.

### Page 45

Paragragh at bottom of the page says, 

    Within this directory, locate the drawable-hdpi, res/drawable-mdpi, and drawable-xhdpi directories.

The middle item should omit "res/".


### Page 51

Same error as Page 37, though text is striked out in the code example here.


### Misc: mQuestionBank vs. mAnswerKey

The instance variable for the list of questions is called mQuestionBank in this chapter. In Chapters 3, 4, and 5, the same variable is called mAnswerKey.

Go with the name you originally typed in - mQuestionBank. Chapters 3, 4, and 5 are incorrect.

## Chapter 3: The Activity Lifecycle

### Page 56 

In the paragraph just above "Using LogCat", onCreate is missing an 'e'.

## Chapter 5: Your Second Activity

### Page 93

A passage says, 

     "You can just create a new file named fragment_crime.xml..." 

The "fragment_crime.xml" filename should be "activity_cheat.xml" instead.

### Page 94 - Listing 5.2

The `android:text` attribute for the first TextView is shown as "@string/warning_text_view". This should instead be `"@string/warning_text"`.

### Page 103 - Listing 5.10

Rename mAnswerKey to mQuestionBank (as originally definied in Chatper 2).

## Chapter 6: Android SDK Versions and Compatibility

### Page 114

Under the "Honeycomb was big" section, second paragraph states, `Given that more than half of devices still run Gingerbread or older devices, developers…`. It should instaed read something like, `Given that more than half of devices still run API levels Gingerbread or older, developers…`

### Page 119 

The code in listings 6.3 and 6.4 should be placed in QuizActivity.java.  The listings are not labeled with the file names.


### Page 119 - Listing 6.4 

The line `actionBar.setSubtitle("TFFTT");` should be replaced with `actionBar.setSubtitle("Bodies of Water");`

Also, this listing hardcodes 11 in the @Target directive: `@TargetApi(11)`.  Using the Build version code constants works as well: `@TargetApi(Build.VERSION_CODES.HONEYCOMB)`.

## Chapter 7: UI Fragments and the Fragment Manager

### Page 136 - Page 138

Some of the newly addded code is not bolded in the listings.  

### Page 138 - Listing 7.6

Contains an extra string definition that was never described. If you follow the book to this point, the file will only contain app_name, hello_world, and menu_settings.  Go ahead and add the title_activity_crime entry while you are at it.

## Chapter 8: Creating User Interfaces with Layouts and Widgets

### Page 151 - Listing 8.3

The EditText includes two new margin attributes that were not previously present. These two attributes should be marked bold in the text.

### Page 152 - Listing 8.5

A passage says,

    Organize your imports to resolve the references to DatePicker and CheckBox.

There is no DatePicker in the listing, so the passage should not mention DatePicker at all.

### Page 159 - Figure 8.6

XML text in the child LinearLayout box doesn't show the required attribute `android:orientation="horizontal"`.  Make sure to add it.  The text talks about selecting horizontal from the palette, but if someone is typing in directly based on Figure 8.6 and don't include the require attribute they will get an error.


## Chapter 18: Context Menus and Contextual Action Mode

### Page 283 - Figure 18.1

The menu text should read "Delete" instead of "Delete Crime".

### Page 286 - Figure 18.2

The menu text should read "Delete" instead of "Delete Crime".

### Page 290 - Listing 18.7
The listing as a whole looks like this:
     
        ...
        listView.setChoiceMode(ListView.CHOICE_MODE_MULTIPLE_MODAL);
        listView.setMultiChoiceModeListener(new MultiChoiceModeListener() {
        ...[lots of code here]...
        });
            
        return v;
     }


It should be inside an else statement, though. So the listing should actually look like this:

            ...
        } else {
            listView.setChoiceMode(ListView.CHOICE_MODE_MULTIPLE_MODAL);
            listView.setMultiChoiceModeListener(new MultiChoiceModeListener() {
                ...[lots of code here]...
            });
        }

        return v;
    }


### Page 297

The ActionBarSherlock challenge omits one key step - you must change the theme for your app to one of the ABS themes (Theme.Sherlock, Theme.Sherlock.Light, or Theme.Sherlock.Light.DarkActionBar), or to a custom theme that inherits from one of those themes. Without this step, your app will not run on older devices. 


## Chapter 21

### Page 348 - Listing 21.2 

The indentation on the following line in the toJSON() method is incorrect: `json.put(JSON_SUSPECT, mSuspect);`.
The method should instead read:

    public JSONObject toJSON() throws JSONException {
        JSONObject json = new JSONObject();
        …
        if (mPhoto != null)
        	json.put(JSON_PHOTO, mPhoto.toJSON());
        json.put(JSON_SUSPECT, mSuspect);
        return json;
    }
    
The bracing is correct around this line; the indentation, however, is not. This line should be indented one indentation level to the left, to be even with "return json;" on the following line.

## Chapter 22: Two-Pane Master-Detail Interfaces

### Page 367 - Listing 22.8

The override for getLayoutResId() looks like this:

    @Override
    protected int getLayoutResId() {
        return R.layout.activity_twopane;
    }

This disagrees with earlier code, which asked you to use R.layout.activity_masterdetail. The earlier code is correct, and activity_masterdetail should be used.  The code in listing 22.8 should instead read:

    @Override
    protected int getLayoutResId() {
        return R.layout.activity_masterdetail;
    }

### Page 369

Just under Figure 22.6, the text says the following: `Right now, you only reload the list immediately after adding a crime…`

Don't have any code that does that? You're not crazy - the text is incorrect here. No such code has been specified in the text so far.

### Page 370 - Listing 22.13 

You see the following code listing:

    public void onCrimeUpdated(Crime crime) {
        FragmentManager fm = getSupportFragmentManager();
        CrimeListFragment listFragment = (CrimeListFragment)
                fm.findFragmentById(R.id.fragmentContainer);
        listFragment.updateUI();
    }

This listing is missing some context - there is no implementation of the interface. The complete listing should be as follows:

    public class CrimeListActivity extends SingleFragmentActivity 
        implements CrimeListFragment.Callbacks, CrimeFragment.Callbacks {

        ...

        public void onCrimeUpdated(Crime crime) {
            FragmentManager fm = getSupportFragmentManager();
            CrimeListFragment listFragment = (CrimeListFragment)
                    fm.findFragmentById(R.id.fragmentContainer);
            listFragment.updateUI();
        }
    }

CrimeFragment.Callbacks at the top and the entire onCrimeUpdated(Crime) implementation should be bolded to indicate this is new code to be added.

### Home icon crash on tablet devices

If you tap the Home icon in the action bar on a tablet, the app will crash. The issue is that CrimeListActivity has no parent activity. 

To fix, add the following code to CrimeFragment.onCreateView:

    public View onCreateView(LayoutInflater inflater, ViewGroup parent, Bundle savedInstanceState) {
        View v = inflater.inflate(R.layout.fragment_crime, parent, false);

        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.HONEYCOMB &&
              NavUtils.getParentActivityIntent(getActivity()) != null) {
            getActivity().getActionBar().setDisplayHomeAsUpEnabled(true);
        }

