# MaterialTwoStageRating
MaterialTwoStageRating is a library to help you promote your android app by prompting users to rate the app after using it for a few days.
Also its two stage process ensures higher reviews to go to playstore while getting useful feedback on lower ratings.

# Screenshots and stages


<img src="https://raw.githubusercontent.com/wimbervoets/MaterialTwoStageRating/master/snapshots/Screenshot_20170102-161620.png" width="200" height="350" />
<img src="https://raw.githubusercontent.com/wimbervoets/MaterialTwoStageRating/master/snapshots/Screenshot_20170102-161628.png" width="200" height="350" />
<img src="https://raw.githubusercontent.com/wimbervoets/MaterialTwoStageRating/master/snapshots/Screenshot_20170102-161834.png" width="200" height="350" />

**Stage 1)** A dialog is displayed to prompt users to rate your app.

**Stage 2)** If user gives 3 or less rating -> A feedback dialog is shown asking users what went wrong?
         If users gives 4 or more rating -> User is requested to rate your app on playstore.

# Install

For gradle, go to your app.gradle file and inside ` dependencies{}` add :

         compile 'be.jatra.materialtwostagerating:library:1.0'

Thats it, you are good to go.

#  Usage

To put it simply, it can be done just in one line of code inside your activity's ' onCreate(...'

         MaterialTwoStageRating.with(this).materialTwoStageRating.showIfMeetsConditions();

It sets the texts (as in above pics) and conditions (5 days of use or 5 times opening of app or 5 times setting of an custom event) to defaults.
         


**( optional)** If you want to change conditions, you can do this insted inside activity's ' onCreate(..'
    
    MaterialTwoStageRating materialTwoStageRating = MaterialTwoStageRating.with(this);
    //initialises condintions to 5 days of use, 10 times of launch use or 5 triggers of custom event.
    materialTwoStageRating.setInstallDays(5).setLaunchTimes(10).setEventsTimes(5);
    
    //If user dismisses it, it simply resets again. (when user dismissed by clicking anywhere else on screen)
    materialTwoStageRating.resetOnDismiss(true);  //it is true by default
    
    //If user gives rating the first time but declines to give playstore rating/ feedback we can reset the
    //MaterialTwoStageRating. These are false by default.
    materialTwoStageRating.resetOnFeedBackDeclined(true).resetOnRatingDeclined(true);
    
    //You may choose to show/hide your app icon in rating prompt (default true)
    materialTwoStageRating.setShowAppIcon(true);
    
    //Finally call to show feedback dialog if any of condition is met.
    materialTwoStageRating.showIfMeetsConditions();
         

'setEventsTime(int n)' sets this dialog on 'n' custom event triggers (like 'n times user clicks a button/ buys a product etc.'). You can increment this trigger anywhere like this:

         MaterialTwoStageRating.with(MainActivity.this).incrementEvent();
         
For now you need to add a feedback listener wherever you want to listen for feedback (see below how). You may want to add a feedback listener to this as well. 
         
         MaterialTwoStageRating.with(MainActivity.this).incrementEvent()
         .setFeedbackReceivedListener(new FeedbackReceivedListener() {
              @Override
              public void onFeedbackReceived(String feedback) {
                  Toast.makeText(MainActivity.this, feedback, Toast.LENGTH_SHORT).show();
                  }
              };
         
**( optional)** On receiving feedback, any action can be done on the feedback using feedbacklistener. There are two types, one with feedback only as an argument and one with feedback and rating as argument.
 
         
         //Feedback listener giving back only the feedback
         materialTwoStageRating.setFeedbackReceivedListener(new FeedbackReceivedListener() {
              @Override
              public void onFeedbackReceived(String feedback) {
                  Toast.makeText(MainActivity.this, feedback, Toast.LENGTH_SHORT).show();
                  }
              }
              
         //Feedback listener with rating information as well
         materialTwoStageRating.setFeedbackWithRatingReceivedListener(new FeedbackWithRatingReceivedListener() {
            @Override
            public void onFeedbackReceived(float rating, String feedback) {
                Toast.makeText(MainActivity.this, "Rating :" + rating + "Feedback :" + feedback, Toast.LENGTH_SHORT).show();
            }
        });
                  

**( optional)**However if you want to costumize all three diologs as per your app specific text, you can do it like this (You may want to include it inside such a function to be called from 'onCreate(.. ':
 
         
         initTwoStage {
                  MaterialTwoStageRating materialTwoStageRating = MaterialTwoStageRating.with(this);
                  //Setting conditions
                  materialTwoStageRating.setInstallDays(5).setEventsTimes(5).setLaunchTimes(5);
                  materialTwoStageRating.resetOnDismiss(true).resetOnFeedBackDeclined(true).resetOnRatingDeclined(false);
                  materialTwoStageRating.showIfMeetsConditions();

                  //Setting feedback listener
                  materialTwoStageRating.setFeedbackReceivedListener(new FeedbackReceivedListener() {
                       @Override
                       public void onFeedbackReceived(String feedback) {
                           Toast.makeText(MainActivity.this, feedback, Toast.LENGTH_SHORT).show();
                       }
                   });

                   //Setting texts for initial prompt
                   materialTwoStageRating.with(this).setRatePromptTitle("INITIAL_TITLE").
                           setRatePromptLaterText("LATER_TEXT").setRatePromptNeverText("NEVER_TEXT").setRatePromptDismissible(false);

                   //Setting texts for confirmation dialog
                   materialTwoStageRating.with(this).setConfirmRateDialogTitle("CONFIRMATION_TITLE").
                   setConfirmRateDialogDescription("CONFIRMATION_DESCRITPION").
                   setConfirmRateDialogPositiveText("POSITIVE_BUTTON_TEXT").
                   setConfirmRateDialogNegativeText("NEGATIVE_BUTTON_TEXT").
                   setConfirmRateDialogDismissible(true);

                   //Setting texts for feedback title
                   materialTwoStageRating.with(this).setFeedbackDialogTitle("FEEDBACK_TITLE").
                   setFeedbackDialogDescription("FEEDBACK_DIALOG_DESCRIPTION").
                   setFeedbackDialogPositiveText("POSITIVE_BUTTON_TEXT").
                   setFeedbackDialogNegativeText("NEGATIVE_BUTTON_TEXT").
                   setFeedbackDialogDismissible(false);
             }


##Contribute
Contributions are welcome. Please open a [pull-request](https://help.github.com/articles/about-pull-requests/).


#Developed By

* Wim Bervoets
 * [about.me/wbervoets](https://about.me/wbervoets)
 * [paypal.me/wimbervoets](https://www.paypal.me/wimbervoets)
* The source code is based on https://github.com/shaileshmamgain5/TwoStageRate


#License

    Copyright 2017 Wim Bervoets

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.



