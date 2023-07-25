# Android_ScoreDemo
- Recorded Score App
![Screenshot_20230725_163345](https://github.com/evelynchang0605/Android_ScoreDemo/assets/137132532/e61decb5-b023-4790-bb7b-41d190f4516a)

- Combine the 'DataBinding' and 'LiveData' functions.

##MyViewModel.java  
- LiveData: You don't need to save the record manually. Can more flexibly refresh the data.  
'''
  private MutableLiveData<Integer> scoreA;
  public MutableLiveData<Integer> getScoreA() {
        if(scoreA == null){
            scoreA = new MutableLiveData<>();
            scoreA.setValue(0);
        }
        return scoreA;
    }
'''  
##Build.Gradle
- Don't forget to add the below sequence.    
'''
  dataBinding.enabled true
'''

##MainActivity.java  
- Using Binding and ViewModel  
'''
  binding = DataBindingUtil.setContentView(this, R.layout.activity_main);
  myViewModel = new ViewModelProvider(this).get(MyViewModel.class);
  binding.setData(myViewModel);
  binding.setLifecycleOwner(this);
'''
##Activity_Main.xml  
- Covert to binding configuration.  
'''
   <data>
        <variable
            name="data"
            type="com.example.recorderdemo.MyViewModel" />

    </data>
 '''   
- Then you can set the UI function as below.  
'''
  android:text="@{String.valueOf(data.scoreA)}"
  android:text="@{String.valueOf(data.scoreB)}"
  android:onClick="@{()->data.teamAadd(1)}"
  android:onClick="@{()->data.teamAadd(2)}"
 ''' 
