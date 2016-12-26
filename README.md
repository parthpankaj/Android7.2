# Android7.2
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:paddingBottom="@dimen/activity_vertical_margin"
    android:paddingLeft="@dimen/activity_horizontal_margin"
    android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    tools:context=".MainActivity" >

    <AutoCompleteTextView
        android:id="@+id/autoCompleteTextView1"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_centerHorizontal="true"
        android:layout_centerVertical="true"
        android:ems="10"
        android:hint="Country Name">

        <requestFocus />
    </AutoCompleteTextView>

    <AutoCompleteTextView
        android:id="@+id/autoCompleteTextView2"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_centerHorizontal="true"
        android:layout_centerVertical="true"
        android:ems="10"
        android:hint="City Code">
    </AutoCompleteTextView>

</RelativeLayout>
------------
package com.example.pankaj.sql72;


        import java.util.HashMap;
        import android.os.Bundle;
        import android.app.Activity;
        import android.util.Log;
        import android.view.Menu;
        import android.view.View;
        import android.widget.ArrayAdapter;
        import android.widget.AutoCompleteTextView;

public class MainActivity extends Activity {
    HashMap<String, String> CountryData;
    HashMap<String, String> CityData;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        CountryData = new HashMap<String, String>();
        CountryData.put("India", "IN");
        CountryData.put("United States", "US");
        CountryData.put("United Kingdom", "GB");
        CountryData.put("Italy", "IT");
        CityData = new HashMap<String, String>();
        CityData.put("City 1", "1");
        CityData.put("City 2", "2");
        CityData.put("City 3", "3");
        CityData.put("City 4", "4");

        setCountries(CountryData.keySet().toArray(new String[0]));
    }

    private void setCountries(String cData[]) {
        ArrayAdapter<String> adapter = new ArrayAdapter<String>(this,
                android.R.layout.simple_dropdown_item_1line, cData);
        final AutoCompleteTextView countryTextView = (AutoCompleteTextView)
                findViewById(R.id.autoCompleteTextView1);
        countryTextView.setThreshold(2);
        countryTextView.setAdapter(adapter);
        countryTextView
                .setOnFocusChangeListener(new View.OnFocusChangeListener() {
                    @Override
                    public void onFocusChange(View view, boolean hasFocus) {
                        if (!hasFocus) {
                            String val = countryTextView.getText() + "";
                            String code = CountryData.get(val);
                            Log.v("activity_main",
                                    "Selected Country Code: " + code);
                            if (code != null) {
                                setCities(CityData.keySet().toArray(
                                        new String[0]));
                            } else {
                                countryTextView.setError("Invalid Country");
                            }
                        }
                    }
                });
    }

    private void setCities(String cData[]) {
        ArrayAdapter<String> adapter = new ArrayAdapter<String>(this,
                android.R.layout.simple_dropdown_item_1line, cData);
        final AutoCompleteTextView cityTextView = (AutoCompleteTextView)
                findViewById(R.id.autoCompleteTextView2);
        cityTextView.setThreshold(2);
        cityTextView.setAdapter(adapter);
        cityTextView.setOnFocusChangeListener(new View.OnFocusChangeListener() {
            @Override
            public void onFocusChange(View view, boolean hasFocus) {
                if (!hasFocus) {
                    String val = cityTextView.getText() + "";
                    String code = CityData.get(val);
                    Log.v("activity_main",
                            "Selected City Code: " + code);
                    if (code == null) {
                        cityTextView.setError("Invalid City");
                    }
                }
            }
        });
    }

    @Override
    public boolean onCreateOptionsMenu(Menu menu) {
        // Inflate the menu; this adds items to the action bar if it is present.
        getMenuInflater().inflate(R.menu.truiton_auto_complete_text_view, menu);
        return true;
    }

}
