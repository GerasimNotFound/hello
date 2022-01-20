package com.example.mykingdom;

import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.LinearLayout;
import android.widget.TextView;
import android.widget.Toast;

import androidx.appcompat.app.AppCompatActivity;

public class Game extends AppCompatActivity {
    Character King;
    protected Story story;
    private TextView status,title,desc;
    private LinearLayout buttons;
    private Situation start_story;
    public Situation current_situation;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        status = this.findViewById(R.id.status);
        title = this.findViewById(R.id.title);
        desc = this.findViewById(R.id.desc);
        buttons = this.findViewById(R.id.buttons);
        King = new Character("Римуру");

        start_story = new Situation("Голод", "Ваше поселение голодает, гоблины умеют только собирать плоды. Возможно, как прибывший с другого мира человек Вы сможете обучить их чему-нибудь\n" +
                    "(1)Не учить гоблинов, найду себе рассу по мощнее.\n" +
                    "(2)Научить воровать у других поселений.\n" +
                    "(3)Научить выращиванию и скотоводству.\n",
                    3, 0, 0, 0);
        start_story.direction[0] = new Situation("Ужасный правитель.", "Вы оставили на гибель своих гоблинов в надежде найти рассу посильнее.\n" +
                    "Но сильным рассам правитель не нужен поэтому Вы потеряли всё!",
                    0,-100, 0,0);
        start_story.direction[1] = new Situation("Пойманы!", "Ваших гоблинов поймали в воровстве!\n" +
                    "Вы не можете больше продолжать развивать ваше государство с таким малым количеством жителей!",
                    0,-50,-1,-50);
        start_story.direction[2] = new Situation("Аграрное общество.","Вы обучили Ваших гоблинов сельскохозяйственному производству.\n" +
                    "Ваше государство больше не голодает!\n" +
                    "К Вашему государству пришли давние враги гоблинов - Магволки.\n" +
                    "(1)Защищаться от волков.\n" +
                    "(2)Вступить с волками в союз.\n",
                    2,100,0,20);
        start_story.direction[2].direction[0] = new Situation("Сильная потеря.", "Вы начали оборонять Ваше государство и потеряли некоторых гоблинов.\n" +
                    "Магволки отступили." +
                    "К Вашему поселению приближается сильная группа бродячих демонологов.\\n\" +\n" +
                    "(1)Поговорить с демонологами.\n" +
                    "(2)Напасть на демонологов.",
                    2,-30,0,-40);
        start_story.direction[2].direction[1] = new Situation("Новые друзья.", "Магволки предложили Вам сразиться с их вожаком!\n" +
                    "Вы смогли одолеть Вашего опонента и вступили в новый союз!!!" +
                    "К Вашему поселению приближается сильная группа бродячих демонологов.\\n\" +\n" +
                    "(1)Поговорить с демонологами.\n" +
                    "(2)Напасть на демонологов.\n",
                    2,100,1, 0);
        start_story.direction[2].direction[0].direction[0] = new Situation("Беженцы.","Демонологи оказались беженцами.\n" +
                    "(1)Приютить демонологов.\n"  +
                    "(2)Пропустить демонологов сквозь город.\n" +
                    "(3)Напасть на демонологов!\n" +
                    "(4)Торговать с демонологами.\n",
                    4,0,0,0);
        start_story.direction[2].direction[1].direction[0] = new Situation("Беженцы.","Демонологи оказались беженцами.\n" +
                    "(1)Приютить демонологов.\n"  +
                    "(2)Пропустить демонологов сквозь город.\n" +
                    "(3)Напасть на демонологов!\n" +
                    "(4)Торговать с демонологами.\n",
                    4,0,0,0);
        start_story.direction[2].direction[0].direction[1] = new Situation("Жестокая битваю","Вы храбро сражались, но демонологи, как одна из выссших расс, вышли победителями.\n" +
                    "Ваш город остался без населения.",
                    0,-500,-2,-100);
        start_story.direction[2].direction[1].direction[1] = new Situation("Жестокая битваю","Вы храбро сражались, но демонологи, как одна из выссших расс, вышли победителями.\n" +
                    "Ваш город остался без населения.",
                    0,-500,-2,-100);
        start_story.direction[2].direction[1].direction[0].direction[0] = new Situation("Новые друзья.", "Демонологи присоединились к Вашему городу.\n" +
                    "Вы построили своё государство.\n",
                    0,500,1,40);
        start_story.direction[2].direction[1].direction[0].direction[1] = new Situation("Варфоломеевская ночь.", "Демонологи вырезали всё Ваше поселение и разграбили город.\n" +
                    "Вы стали жертвой обмана в этом мире.\n",
                    0,-100,-2,-100);
        start_story.direction[2].direction[1].direction[0].direction[2] = new Situation("Жестокая битваю","Вы храбро сражались, но демонологи, как одна из выссших расс, вышли победителями.\n" +
                    "Ваш город остался без населения.",
                    0,-500,-2,-100);
        start_story.direction[2].direction[1].direction[0].direction[3] = new Situation("Грабители.","Демонологи, узнав, что у гоблинов и магволков есть ресурсы, решили разграбить ваше поселение\n" +
                    "Ваш город остался без ресурсов.",
                    0,-100,-2,-100);
        start_story.direction[2].direction[0].direction[0].direction[0] = new Situation("Новые друзья.", "Демонологи присоединились к Вашему городу.\n" +
                    "Вы построили своё государство.\n",0,500,1,40);
        start_story.direction[2].direction[0].direction[0].direction[1] = new Situation("Варфоломеевская ночь.", "Демонологи вырезали всё Ваше поселение и разграбили город.\n" +
                    "Вы стали жертвой обмана в этом мире.\n",0,-100,-2,-100);
        start_story.direction[2].direction[0].direction[0].direction[2] = new Situation("Жестокая битваю","Вы храбро сражались, но демонологи, как одна из выссших расс, вышли победителями.\n" +
                    "Ваш город остался без населения.",
                    0,-500,-2,-100);
        start_story.direction[2].direction[0].direction[0].direction[3] = new Situation("Грабители.","Демонологи, узнав, что у гоблинов и магволков есть ресурсы, решили разграбить ваше поселение\n" +
                    "Ваш город остался без ресурсов.",
                    0,-100,-2,-100);
        current_situation = start_story;
    }
    @Override
    protected void onResume() {
        super.onResume();
        showSituation(story.current_situation);
    }

    public void showSituation(Situation situation){
        buttons.removeAllViews();
        King.Rep += story.current_situation.dRep;
        King.Unions += story.current_situation.dUn;
        King.Population += story.current_situation.dPop;
        status.setText("<============\n" +
                "Ваша Репутация:"+
                King.Rep + "\n" +"Ваши союзы:" + King.Unions + "\n"+"Ваша популяция:" + King.Population + "\n" + "============>\n");
        title.setText("<==========="
                + story.current_situation.subject + "============>");
        desc.setText(story.current_situation.text);

        for (int i = 0; i < situation.direction.length; i++) {
            final int answer = i;
            Button b = new Button(getBaseContext());
            b.setText(i+1+"");
            b.setOnClickListener(new View.OnClickListener() {
                @Override
                public void onClick(View v) {
                    showSituation(situation.direction[answer]);
                }
            });
            buttons.addView(b);

            }
        if (story.current_situation.direction.length == 0){
            Button b = new Button(getBaseContext());
            b.setText("Выйти");
            b.setOnClickListener(new View.OnClickListener() {
                @Override
                public void onClick(View v) {
                    finish();
                }
            });
            buttons.addView(b);
        }
    }
}
