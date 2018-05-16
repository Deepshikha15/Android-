# Android-

package com.example.deepshikha.birthdaycard;

import android.support.v7.app.AppCompatActivity;
import android.view.KeyEvent;
import android.os.Bundle;
import android.app.Activity;
import android.view.View;
import android.widget.ArrayAdapter;
import android.widget.Button;
import android.widget.EditText;
import android.widget.ListView;

import java.util.ArrayList;

public class MainActivity extends AppCompatActivity {
    private EditText etInput;
    private Button btnAdd;
    private ListView lvItem;
    private ArrayList<String> itemArr;
    private ArrayAdapter<String> itemAdapter;


    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        setUpView();
    }

    private void setUpView() {
        etInput = this.findViewById(R.id.editText_input);
        btnAdd = this.findViewById(R.id.button_add);
        lvItem = this.findViewById(R.id.listView_items);



        itemArr = new ArrayList<>();
        itemArr.add("Abhijeet");
        itemArr.add("Gairola");

        itemAdapter = new ArrayAdapter<>(this, android.R.layout.simple_list_item_1,itemArr);
        lvItem.setAdapter(itemAdapter);




        btnAdd.setOnClickListener(new View.OnClickListener() {
            public void onClick(View v) {
                addItemList();
            }
        });

        etInput.setOnKeyListener(new View.OnKeyListener() {
            public boolean onKey(View v, int keyCode, KeyEvent event) {
                if (keyCode == KeyEvent.KEYCODE_ENTER) {
                    addItemList();
                }
                return true;
            }
        });
    }

    protected void addItemList() {
        if (isInputValid(etInput)) {
            itemArr.add(0,etInput.getText().toString());
            etInput.setText("");
            itemAdapter.notifyDataSetChanged();
        }
    }

    protected boolean isInputValid(EditText etInput2) {
        if (etInput2.getText().toString().trim().isEmpty()) {
            etInput2.setError("Please Enter Item");
            return false;
        } else {
            return true;
        }
    }


}
