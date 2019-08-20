public void onCreate(Bundle savedInstanceState) {
super.onCreate(savedInstanceState);
setContentView(R.layout.main);
mList = (ListView) findViewById(R.id.main_list);
mVoteList = (ListView) findViewById(R.id.main_vote_list);
 
ArrayList<VoteBean> mData = new ArrayList<VoteBean>();
for(int i = 0;i<5;i++){
VoteBean bean = new VoteBean();
bean.setTitle("选项" + (char)(65+i));
bean.setIsCheck(false);
mData.add(bean);
}
mVoteTopAdapter = new VoteTopAdapter(this,mData);
mList.setAdapter(mVoteTopAdapter);
 
ArrayList<String> mVoteData = new ArrayList<String>();
mVoteData.add("http://www.aivtp.com/");
mVoteData.add("");
mVoteData.add("");
mVoteData.add("");
mVoteAdapter = new VoteDetailAdapter(this,mVoteData);
mVoteList.setAdapter(mVoteAdapter);
 
 
// 这里把点击的监听设成条目的监听，如果只是想点击checkbox选择，可以注释这段，把adapter注释的那段解除
// TODO 这里需要注意的是，条目里面有checkbox 会获得焦点，使得 list的 条目监听没有作用
// TODO 解决方法是
/**
* 我们可以通过对Item Layout的根控件设置其android:descendantFocusability=”blocksDescendants”即可，
* 这样Item Layout就屏蔽了所有子控件获取Focus的权限，不需要针对Item Layout中的每一个控件重新设置focusable属性了，
* 如此就可以顺利的响应onItemClickListener中的onItenClick()方法了。
* 例如我的ListViw的每个item项是RelativeLayout，
* 那么我就可以设置RelativeLayout的android:descendantFocusability=”blocksDescendants”即可。
* 注意：这个属性不能设置给ListView，设置了也不起作用
*/
mList.setOnItemClickListener(new AdapterView.OnItemClickListener() {
@Override
public void onItemClick(AdapterView<?> adapterView, View view, int i, long l) {
if (index == i){
index = -1;
}else{
index = i;
}
mVoteTopAdapter.notifyDataSetChanged();
Toast.makeText(MyActivity.this,"选项" + (i+1),Toast.LENGTH_SHORT).show();
}
});
 
}
