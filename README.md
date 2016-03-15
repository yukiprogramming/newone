# newone
import android.net.Uri;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.widget.Button;
import android.widget.EditText;
import android.widget.TextView;
import android.view.View.OnClickListener;

import com.google.android.gms.appindexing.Action;
import com.google.android.gms.appindexing.AppIndex;
import com.google.android.gms.common.api.GoogleApiClient;


public class SimpleQuizMainActivity extends AppCompatActivity {
    private int currentQuestion;
    private String[] questions;
    private String[] answers;

    private Button answerButton;
    private Button questionButton;
    private TextView questionView;
    private TextView answerView;
    private EditText answerText;
    /**
     * ATTENTION: This was auto-generated to implement the App Indexing API.
     * See https://g.co/AppIndexing/AndroidStudio for more information.
     */
    private GoogleApiClient client;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_simple_quiz_main);
        init();
        // ATTENTION: This was auto-generated to implement the App Indexing API.
        // See https://g.co/AppIndexing/AndroidStudio for more information.
        client = new GoogleApiClient.Builder(this).addApi(AppIndex.API).build();
    }

    public void init() {
        questions = new String[]{"What is the capital of Egypt?",
                "What class are you in right now?"};
        answers = new String[]{"Cairo", "IST380"};
        currentQuestion = -1;
        answerButton = (Button) findViewById(R.id.AnswerButton);
        questionButton = (Button) findViewById(R.id.QuestionButton);
        questionView = (TextView)
                findViewById(R.id.QuestionTextView);
        answerView = (TextView) findViewById(R.id.AnswerTextView);
        answerText = (EditText) findViewById(R.id.AnswerText);
        answerButton.setOnClickListener(new OnClickListener() {
            @Override
            public void onClick(android.view.View v) {

            }
        });
        questionButton.setOnClickListener(new OnClickListener() {
            @Override
            public void onClick(android.view.View v) {

            }

        });
    }


    /*
    * This method
    * 1: increment currentQuestion index
    * 2: check if it is equal to the size of the array and rest if necessary
    * 3: display the question at currentQuestion index in question view
    * 4: Empty answer view
    */
    public void showQuestion() {
        currentQuestion++;
        if (currentQuestion == questions.length)
            currentQuestion = 0;
        questionView.setText(questions[currentQuestion]);
        answerView.setText("");
        answerText.setText("");
    }

    /*
    * This method return true if the answer equals to correct answer
    * (Ignoring case)
    */
    public boolean isCorrect(String answer) {
        return (answer.equalsIgnoreCase(answers[currentQuestion]));
    }

    /* this method :
    * 1: Read the text ( answer) from the answerTextEdit
   * 2: call the isCorrect method
   * 3: display the appropriate message.
   */
    public void checkAnswer() {
        String answer = answerText.getText().toString();
        if (isCorrect(answer))
            answerView.setText("You're right!");
        else
            answerView.setText("Sorry, the correct answer is " + answers[currentQuestion]);
    }


    @Override
    public void onStart() {
        super.onStart();

        // ATTENTION: This was auto-generated to implement the App Indexing API.
        // See https://g.co/AppIndexing/AndroidStudio for more information.
        client.connect();
        Action viewAction = Action.newAction(
                Action.TYPE_VIEW, // TODO: choose an action type.
                "SimpleQuizMain Page", // TODO: Define a title for the content shown.
                // TODO: If you have web page content that matches this app activity's content,
                // make sure this auto-generated web page URL is correct.
                // Otherwise, set the URL to null.
                Uri.parse("http://host/path"),
                // TODO: Make sure this auto-generated app deep link URI is correct.
                Uri.parse("android-app://com.example.yuki.simplequiz/http/host/path")
        );
        AppIndex.AppIndexApi.start(client, viewAction);
    }

    @Override
    public void onStop() {
        super.onStop();

        // ATTENTION: This was auto-generated to implement the App Indexing API.
        // See https://g.co/AppIndexing/AndroidStudio for more information.
        Action viewAction = Action.newAction(
                Action.TYPE_VIEW, // TODO: choose an action type.
                "SimpleQuizMain Page", // TODO: Define a title for the content shown.
                // TODO: If you have web page content that matches this app activity's content,
                // make sure this auto-generated web page URL is correct.
                // Otherwise, set the URL to null.
                Uri.parse("http://host/path"),
                // TODO: Make sure this auto-generated app deep link URI is correct.
                Uri.parse("android-app://com.example.yuki.simplequiz/http/host/path")
        );
        AppIndex.AppIndexApi.end(client, viewAction);
        client.disconnect();
    }
}
