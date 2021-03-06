Bash shell scripts, Python scripts and some data for practical work of Multilayer Perceptron classification with Myanmar fingerspelling images (Ka to Nga Consonants).

အောက်ပါ ပရိုဂရမ်တွေကို သုံးပြီး image classification ကို လက်တွေ့ လုပ်ကြည့်ကြရအောင်
extract-feature.sh (for feature extraction)
add-label.sh (for adding y labels, combining all features as one file for training)
train-test-MLP-clf.py (for training image classifier and testing)

==========

အရင်ဆုံး ./data/ ဖိုလ်ဒါကို mkdir data ဆိုတဲ့ command ပေးပြီး ဖိုလ်ဒါ အသစ်ဆောက်ပါ။
အဲဒီအောက်မှာ ကိုယ်က classification လုပ်ချင်တဲ့ image ဖိုင်တွေကို သက်ဆိုင်ရာ class အလိုက် sub-folder တွေခွဲပြီး သိမ်းပါ။
ကိုယ် ကြိုက်တဲ့ ပုံတွေနဲ့ classification စမ်းလုပ်ကြည့်လို့ ရပါတယ်။
class အရေအတွက်ကလည်း ကိုယ်ကြိုက်သလို ထားလို့ ရပါတယ်။

ဥပမာ classifier မော်ဒယ်ကို training လုပ်ချင်တဲ့ class က "ကကြီး" ကနေ "င" အထိ ၅မျိုးရှိတယ်ဆိုရင်၊ အောက်ပါအတိုင်း ဖိုလ်ဒါ ၅ခုရှိရမယ်။

lar@lar-air:~/experiment/fs/mc-fs/ucsy-fs/data$ ls
Ga  Gha  Ka  Kha  Nga 

Ka/ အောက်မှာ ကကြီး ပုံတွေ
Kha/ အောက်မှာ ခကွေး ပုံတွေ
Ga/ အောက်မှာ ဂငယ် ပုံတွေ
Gha/ အောက်မှာ ဃ ပုံတွေ
Nga/ အောက်မှာ င ပုံတွေ ကို အသီးသီး သိမ်းထားပါ။

UCSY ရဲ့ Neural Network class မှာက မိုဘိုင်းဖုန်း ၂လုံးကို သုံးပြီး ပုံ ၁၈၀ ကို ရိုက်ယူခဲ့ပါတယ်။
အဲဒီပုံတွေကိုလည်း သုံးချင်ရင် သုံးလို့ရအောင် ./data ဖိုလ်ဒါအောက်မှာ တင်ပေးထားပါတယ်။

==========

./caffe-model/ အောက်မှာ caffe နဲ့ သက်ဆိုင်တဲ့ ဖိုင် ၃ဖိုင်ရှိနေရပါမယ်။
bvlc_reference_caffenet.caffemodel ဖိုင်က ဖိုင်ဆိုက်ကြီးလို့ GitHub မှာ မတင်ထားပါဘူး။
အောက်ပါ လင့် ကနေ ဒေါင်းလုဒ်လုပ်ယူပါ။
https://github.com/BVLC/caffe/tree/master/models/bvlc_reference_caffenet

==========

./data နဲ့ ./caffe-model ဖိုလ်ဒါပြင်ဆင်တာပြီးပြီ ဆိုရင်run ကြည့်လို့ ရပြီ။

==========

Running Steps:

Feature extraction လုပ်တဲ့ အဆင့် :
$time ./extract-feature.sh ./data/ | tee train-test.log

train လုပ်လို့ရအောင် တစ်ပုံချင်းစီရဲ့ feature တွေကို ဖိုင်တစ်ဖိုင်ထဲမှာ လေဘယ် (နောက်ဆုံး ကော်လံမှာရှိ) တပ်ပြီး သိမ်းတဲ့ အလုပ်ကို လုပ်ဖို့၊
နောက်ပြီးတော့ id နဲ့ class name dictionary ဆောက်တဲ့ အလုပ်ကို လုပ်ဖို့အတွက်က အောက်ပါ command ကို run ပါ။
$./add-label.sh ./data/ | tee ./train-test.log 

Multilayer perceptron (MLP) နဲ့ classifier modeling (i.e. training) နဲ့ testing ကို လုပ်ဖို့အတွက်က အောက်ပါ command ကို run ပါ။ 
$python ./train-test-MLP-clf.py ./data/data.feature | tee ./train-test.log 

==========

အထက်မှာ ဥပမာ အနေနဲ့ run ပြထားတဲ့ command တွေမှာ "| tee ./train-test.log" ဆိုပြီး သုံးထားတာက log ဖိုင်အနေနဲ့ သိမ်းဖို့အတွက်ပါ။  
run တဲ့ အခါ စကရင်မှာ မြင်ရတဲ့ output စာကြောင်းတွေကို ./train-test.log ဆိုတဲ့ ဖိုင်မှာ append လုပ်ပြီး သိမ်းပေးဖို့ အတွက် သုံးထားတာပါ။  
မလိုရင် ဖြုတ်ထားခဲ့လို့ ရပါတယ်။  
ကျွန်တော်ကတော့ အမြဲလိုလို experiment လုပ်ရင် log ဖိုင်မှာ သိမ်းထားလေ့ရှိပါတယ်။  
run နေစဉ်မှာ error တစ်ခုခုဖြစ်ရင် debug လုပ်ဖို့ အတွက် အသုံးဝင်တာကော၊ နောက်ပိုင်း ပြန်ကြည့်တဲ့ အခါမှာ ဘာတွေလုပ်ခဲ့တယ်ဆိုတာကို မေ့နေရင်တောင် အသုံးဝင်လို့ပါ။  


