# �e�s���{���̐���l�����ځi�吳9�N�`����12�N�j


Copyright (c) 2020 Michio Inoue




�܂� [e-Stat](https://www.e-stat.go.jp/stat-search/files?page=1&layout=datalist&toukei=00200524&tstat=000000090001&cycle=0&tclass1=000000090004&tclass2=000000090005&stat_infid=000000090265) �̃y�[�W����f�[�^���_�E�����[�h���܂��B




`05k5-5.xlsx` �Ƃ����t�@�C�����{�X�N���v�g�Ɠ����t�H���_�Ƀ_�E�����[�h���ꂽ�Ɖ��肵�܂��B


```matlab
addpath("../../function")
```
# �f�[�^�ǂݍ���


�U�N���ƃC���|�[�g�c�[������ǂݍ��ރX�N���v�g�����܂����B�ϐ� `k55` �Ƃ��ēǂݍ��܂��͂��B


```matlab
importData
```
# �f�[�^����


���n��f�[�^�� `timetable` �^���֗��Ȃ̂ł�����ł܂Ƃ߂Ă݂܂��B




���F����̓f�[�^���傫�������Ă���Ƃ��낪����̂ŏ����Ă��܂��B


```matlab
% k55 ����K�v�ȕ��������o���܂��B
years = [k55{1,3:end}]'; % �N��
names = string(k55(4:end-1,1)); % �s���{���̖��O
data = cell2mat(k55(4:end-1,3:end)); % �l���i���l�����j

% �N�f�[�^�� datetime �^�ɕύX
timeStamp = datetime(years,1,1);
timeStamp.Format = 'yyyy'; % �\���� yyyy�N

% timetable �^�̃f�[�^�쐬
T = array2timetable(data','RowTimes',timeStamp);
T.Properties.VariableNames = names; % �ϐ����w��
```
# �v���b�g�`��
```matlab
barChartRace(T);
```

![figure_0.png](Example_images/figure_0.png)



�S�f�[�^�v���b�g����Ɖ���������������܂���ˁB


## �e�I�v�V�����̉���i�ꕔ�j


�ڍׂ�


```matlab
help barChartRace
```


�ŕ\�����邩�AREADME.md �Ŋm�F���������B


```matlab
barChartRace(T,'NumDisplay',15,'NumInterp',4,...
    'Position',[ 500 60 470 470],'ColorGroups',repmat("g",length(names),1),...
    'XlabelName',"���15�s���{���̐l���i��l�j",'GenerateGIF',false);
```

![figure_1.png](Example_images/figure_1.png)



�g�p�����I�v�V�����̈Ӗ��͈ȉ��F



   -  NumDisplay: ��ʉ��ʂ܂ŕ\�����邩�B����l�͑S�f�[�^�\���ł��B 
   -  NumInterp: �f�[�^�̓��}�_���B�������������炩�ɐ��ڂ��܂��B����l�� 2�B 
   -  Position: �쐬����� Figure �̑傫���B 
   -  ColorGroups: �F�����̎w��B������͉��ł��ǂ��ł����A���������������F�ŕ`���܂��B����l�͂��ׂẴo�[�� 7 �F�ŕ����܂��B 
   -  XlabelName: x���̖��O�B����l�͋�i�����\�����܂���j 
   -  GenerateGIF: `true` �� gif �t�@�C���������܂��B����l�� `false` �ł��B 

# ���͂����l�z��̃P�[�X


`barChartRace` �֐��͐��l�f�[�^�i2�����z��j���󂯕t���܂��B�c���������ԕω�


```matlab
data = T.Variables;
```


�Ő��l�����������o�����ϐ����g���Ă݂܂��B


```matlab
data = T.Variables;
barChartRace(data);
```

![figure_2.png](Example_images/figure_2.png)



�ϐ��̖��O�͓K���� name(���l) �ŕ`����܂��B���ԏ�񂪖����̂ō����������̐��l�i���Ԗڂ̃f�[�^���j�ɂȂ��Ă��܂��B�I�v�V�������g���Ă݂܂��B


## �e�I�v�V�����̉���i�ꕔ�j
```matlab
barChartRace(data,'NumDisplay',15,'LabelNames',names,...
    'Position',[500 60 470 470],'ColorGroups',repmat("g",length(names),1),...
    'XlabelName',"���15�s���{���̐l���i��l�j",'GenerateGIF',false);
```

![figure_3.png](Example_images/figure_3.png)


   -  LabelNames: `timetable` �^�܂��� `table` �^�ϐ��̏ꍇ�͕ϐ��̖��O�����̂܂܎g���܂����A���̃I�v�V�����Ŏw�肷�邱�Ƃ��\�ł��B 
   -  Position: �쐬����� Figure �̑傫���B 
   -  ColorGroups: �F�����̎w��B������͉��ł��ǂ��ł����A���������������F�ŕ`���܂��B 
   -  XlabelName: x���̖��O�B 
   -  GenerateGIF: `true` �� gif �t�@�C���������܂��B����ł� `false` �ł��B 

