# NotePad
This is an AndroidStudio rebuild of google SDK sample NotePad
# 基本功能一 时间戳   
思路： 修改时间的字段在notepad已经存在 只需要修改一下projection把 modifytime显示出来       
   private static final String[] PROJECTION = new String[] {  
            NotePad.Notes._ID, // 0  
            NotePad.Notes.COLUMN_NAME_TITLE,  
            NotePad.Notes.COLUMN_NAME_MODIFICATION_DATE// 1  
    };  
     String[] dataColumns = { NotePad.Notes.COLUMN_NAME_TITLE, NotePad.Notes.COLUMN_NAME_MODIFICATION_DATE} ;  
     并在布局文中添加一个用于显示时间的textview  
     int[] viewIDs = { android.R.id.text1,android.R.id.text2 };  
     
![Alt text](https://github.com/fjnuzyl/notepad/blob/master/images/time.jpg)  

# 基本功能二 查询功能  
思路： 在list_options_menu中一个menuitem 在onOptionsItemSelected方法中的switch里添加  
  case R.id.menu_search:  
              android.app.AlertDialog.Builder builder = new android.app.AlertDialog.Builder(this);  
              final   View view2 = View.inflate(this, R.layout.search_dialog, null);  
              final Button button = (Button) view2.findViewById(R.id.Button);  
              final EditText search_text = (EditText) view2.findViewById(R.id.editText);  
              builder.setTitle("Search").setView(view2);  
              final AlertDialog alertDialog = builder.create();  
              button.setOnClickListener(new View.OnClickListener() {  
                  @Override  
                  public void onClick(View v) {  
                      String text= search_text.getText().toString();  
                      String[] search = {"_id", NotePad.Notes.COLUMN_NAME_TITLE,  
                              NotePad.Notes .COLUMN_NAME_CREATE_DATE};  
                      String selection = NotePad.Notes.COLUMN_NAME_TITLE + " like?";  
                      String[] selectionArgs = {text + "%"};  
                      Cursor cursors = managedQuery(getIntent().getData(),  
                              search,  
                              selection,  
                              selectionArgs,  
                              NotePad.Notes.DEFAULT_SORT_ORDER);  
                      cursors.moveToFirst();  
                      String[] data = {  
                              NotePad.Notes.COLUMN_NAME_TITLE,  
                              NotePad.Notes  
                                      .COLUMN_NAME_CREATE_DATE  
                      };   
                      int[] viewIDs = { android.R.id.text1,android.R.id.text2 };  
                      SimpleCursorAdapter adapters = new SimpleCursorAdapter(  
                              NotesList.this,  
                              R.layout.noteslist_item,  
                              cursors, data, viewIDs);  
                      setListAdapter(adapters);  
                      alertDialog.dismiss();  
                  }  
  
              });  
              alertDialog.show();
根据alterdialog中的editor的文本查询对应的标题  
 
![Alt text](https://github.com/fjnuzyl/notepad/blob/master/images/searchthree.jpg)  

![Alt text](https://github.com/fjnuzyl/notepad/blob/master/images/searchtwo.jpg)  

# 附加功能美化ui  
思路 更改主体  
   <activity android:name="NotesList"  
            android:theme="@android:style/Theme.Holo"  
            android:background="#ffffff"  
            
   ![Alt text](https://github.com/fjnuzyl/notepad/blob/master/images/theme.jpg)  
   
 # 附加功能 更改背景颜色    
 思路  根据 getListView().setBackgroundColor(Color);更改背景颜色  
 在list_options_menu中一个menuitem 取名为color 在onOptionsItemSelected方法中的switch里添加  
   case R.id.color:  
                android.app.AlertDialog.Builder builder2 = new android.app.AlertDialog.Builder(this);  
                final   View view3 = View.inflate(this, R.layout.changecolor, null);  
                builder2.setTitle("Changing Color").setView(view3);  
                final AlertDialog ad = builder2.create();  
                TextView color_Blue = (TextView)view3.findViewById(R.id.Blue);  
                TextView color_LightBlue = (TextView)view3.findViewById(R.id.LightBlue);  
                TextView color_Pink = (TextView)view3.findViewById(R.id.Pink);  
                TextView color_White = (TextView)view3.findViewById(R.id.White);  
                TextView color_Red= (TextView)view3.findViewById(R.id.Red);  
                ad.show();  
                color_Blue.setOnClickListener(new View.OnClickListener() {  
                    @Override  
                    public void onClick(View v) {  
                        preferencescolor="#7A67EE";  
                        getListView().setBackgroundColor(Color.parseColor(preferencescolor));  
                        ad.dismiss();  
                    }  
                });  
                color_LightBlue.setOnClickListener(new View.OnClickListener() {  
                    @Override  
                    public void onClick(View v) {  
                        preferencescolor="#AEEEEE";  
                        getListView().setBackgroundColor(Color.parseColor(preferencescolor));  
                        ad.dismiss();  
                    }  
                });  
                color_Pink.setOnClickListener(new View.OnClickListener() {  
                    @Override  
                    public void onClick(View v) {  
                        preferencescolor="#CD69C9";  
                        getListView().setBackgroundColor(Color.parseColor(preferencescolor));  
                        ad.dismiss();  
                    }  
                });  
                color_White.setOnClickListener(new View.OnClickListener() {  
                    @Override   
                    public void onClick(View v) {  
                        preferencescolor="#FCFCFC";  
                        getListView().setBackgroundColor(Color.parseColor(preferencescolor));  
                        ad.dismiss();  
                    }  
                });  
                color_Red.setOnClickListener(new View.OnClickListener() {  
                    @Override  
                    public void onClick(View v) {  
                        preferencescolor="#FF0000";  
                        getListView().setBackgroundColor(Color.parseColor(preferencescolor));  
                        ad.dismiss();  
                    }  
                });  
                return true;  
                 
               ![Alt text](https://github.com/fjnuzyl/notepad/blob/master/images/color.jpg)  
               
