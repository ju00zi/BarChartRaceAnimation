# Bar Chart Race ���v���b�g���Ă݂悤: ������


Copyright 2020 Michio Inoue




���� Markdown �� [minoue-xx/livescript2markdown](https://github.com/minoue-xx/livescript2markdown) ���g���ă��C�u�X�N���v�g���玩���������Ă��܂��B


# �͂��߂�


�e�f�[�^�̎��n��ω������ʂƂƂ��ɕ\������v���b�g�ABar Chart Race�B




Part 1 �ł� `barh` �֐����g���� Bar Char Race �������ł��������m�F���Ă݂܂����B`BarWidth` �v���p�e�B�̎g�������̂ł����ˁB����͎����҂Ƃ��Ď��ۂɂ��̓���iGIF) ���쐬����Ƃ���܂ł�������܂��B�g�p��ƃ|�C���g�����ɍi���Ă��Љ�܂��B


  
### ���s��


R2019b �ō��܂������A���ŉ������ Arguments �Ɋւ�镔������菜���� R2017b �ł������Ǝv���܂��B




![image_0.png](barChartRaceExample_part2JP_images/image_0.gif)


# �g�p��F�e�s���{���̐���l�����ځi�吳9�N�`����12�N�j


�܂� [e-Stat](https://www.e-stat.go.jp/stat-search/files?page=1&layout=datalist&toukei=00200524&tstat=000000090001&cycle=0&tclass1=000000090004&tclass2=000000090005&stat_infid=000000090265) �̃y�[�W����Y���f�[�^���_�E�����[�h���āA`05k5-5.xlsx` �Ƃ����t�@�C�����{�X�N���v�g�Ɠ����t�H���_�Ƀ_�E�����[�h���ꂽ�Ɖ��肵�܂��B


## Step 1: �f�[�^�ǂݍ���


�U�N���ƃC���|�[�g�c�[������ǂݍ��ރX�N���v�g�����܂����B




![image_1.png](barChartRaceExample_part2JP_images/image_1.png)




�u���݂̃t�H���_�v�ɕ\������� `05k5-5.xlsx` ���_�u���N���b�N���āA�ǂݍ��ݔ͈͂��w�肵�āu�X�N���v�g�̐����v���N���b�N�B�o�̓^�C�v�� cell �z��ŁB




���̃X�N���v�g�����s����ƕϐ� `k55` �Ƃ��ēǂݍ��܂��͂��B�iimportData.m ��[������](https://github.com/minoue-xx/BarChartRaceAnimation/tree/master/example/RegionalPopulationJapan)�ɂ������Ă��܂��B�j


```matlab
importData
```
## Step 2: �f�[�^����


���n��f�[�^�� `timetable` �^�ł܂Ƃ߂�ƕ֗��B���F����̓f�[�^���傫�������Ă���Ƃ��낪����̂ŏ����Ă��܂��B


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


����Ȋ����̃f�[�^�ɂȂ�܂��B


```matlab
head(T)
```
| |Time|�k �C ��|�� �X ��|�� �� ��|�{ �� ��|�H �c ��|�R �` ��|�� �� ��|�� �� ��|�� �� ��|�Q �n ��|�� �� ��|�� �t ��|�� �� �s|�_�ސ쌧|�V �� ��|�x �R ��|�� �� ��|�� �� ��|�R �� ��|�� �� ��|�� �� ��|�� �� ��|�� �m ��|�O �d ��|�� �� ��|�� �s �{|�� �� �{|�� �� ��|�� �� ��|�a�̎R��|
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
|1|1920|2359|756.0000|846.0000|962|899.0000|969|1363|1350|1046|1053|1320|1336|3699|1323|1776|724.0000|747.0000|599.0000|583.0000|1563|1070|1550|2090|1069|651.0000|1287|2588|2302|565.0000|750.0000|
|2|1921|2.3859e+03|767.4000|855.3000|978|904.5000|979.6000|1.3815e+03|1.3557e+03|1.0542e+03|1.0623e+03|1.3303e+03|1.3355e+03|3.8307e+03|1359|1.7907e+03|724.7000|748.0000|602.0000|585.8000|1.5787e+03|1.0838e+03|1.5739e+03|2.1278e+03|1.0656e+03|653.2000|1.3062e+03|2.6866e+03|2.3316e+03|568.3000|757.5000|
|3|1922|2.4169e+03|775.1000|865.1000|992.1000|931.9000|986.6000|1.3859e+03|1.3666e+03|1.0645e+03|1.0708e+03|1.3411e+03|1.3543e+03|3.9842e+03|1.3808e+03|1.7993e+03|723.2000|748.8000|597.8000|589.0000|1.5858e+03|1.0949e+03|1.5964e+03|2.1696e+03|1.0677e+03|655.7000|1.3303e+03|2.7793e+03|2.3637e+03|572.3000|764.3000|
|4|1923|2.4489e+03|784.3000|880.8000|1.0225e+03|940.1000|1.0023e+03|1416|1.3892e+03|1084|1.0937e+03|1.3677e+03|1.3821e+03|3.8594e+03|1.3539e+03|1.8257e+03|733.1000|749.6000|600.3000|592.5000|1.6025e+03|1.1133e+03|1.6267e+03|2.2392e+03|1.0882e+03|658.4000|1.3614e+03|2.9269e+03|2.4091e+03|577.0000|776.0000|
|5|1924|2.4682e+03|792.1000|888.3000|1.0356e+03|926.7000|1.0107e+03|1426|1.3986e+03|1.0915e+03|1.1073e+03|1380|1.3957e+03|4.1855e+03|1.3736e+03|1.8397e+03|741.6000|750.1000|603.6000|595.0000|1.6154e+03|1.1215e+03|1.6437e+03|2.2738e+03|1.0958e+03|660.0000|1388|2.9983e+03|2.4248e+03|579.6000|780.4000|
|6|1925|2499|813.0000|901.0000|1044|936.0000|1027|1438|1409|1090|1119|1394|1399|4485|1417|1850|749.0000|751.0000|598.0000|601.0000|1629|1133|1671|2319|1108|662.0000|1406|3060|2455|584.0000|788.0000|
|7|1926|2556|825.2000|914.8000|1064|937.5000|1.0409e+03|1.4647e+03|1.4254e+03|1.0992e+03|1.1226e+03|1.4121e+03|1.4172e+03|4.6944e+03|1.4539e+03|1.8636e+03|758.2000|752.1000|597.0000|603.7000|1.6494e+03|1.1465e+03|1702|2.3695e+03|1.1146e+03|668.3000|1.4359e+03|3.1603e+03|2.4946e+03|580.7000|796.9000|
|8|1927|2.6121e+03|836.5000|928.6000|1.0815e+03|947.1000|1.0524e+03|1.4766e+03|1.4397e+03|1.1071e+03|1.1524e+03|1.4249e+03|1.4266e+03|4.8974e+03|1.4959e+03|1.8807e+03|762.6000|753.1000|600.4000|609.1000|1.6659e+03|1.1538e+03|1.7231e+03|2.4146e+03|1.1196e+03|673.5000|1462|3260|2.5311e+03|585.6000|803.5000|

## Step 3: �v���b�g


�����܂ł����


```matlab
barChartRace(T);
```


��OK!




�����A�S�f�[�^�v���b�g����Ɖ���������������܂���̂ŁA�I�v�V�������������g���Ă݂܂��B


```matlab
barChartRace(T,'NumDisplay',6,'NumInterp',4,...
    'Position',[500 60 470 370],'ColorGroups',repmat("g",length(names),1),...
    'XlabelName',"���6�s���{���̐l���i��l�j",...
    'GenerateGIF',true,"Outputfilename",'top5.gif');
```


�Ǝ��s����ƁA�`���� GIF ���o���オ��B


## �e��I�v�V����


�ڍׂ� GitHub �� [README.md](https://github.com/minoue-xx/BarChartRaceAnimation/blob/master/README.md) ��


```matlab
help barChartRace
```


�Ō��Ă��炢������ł����A�Ⴆ��



   -  `'NumDisplay'`: ��ʉ��ʂ܂ŕ\�����邩�idefault: �S���j 
   -  `'FontSize'`: �v���b�g�Ŏg���̃t�H���g�T�C�Y�idefault: 15�j 
   -  `'GenerateGIF'`: GIF ���o�͂��邩�ǂ����idefaiut: false�j 
   -  `'LabelNames'`: `timetable` �^�܂��� `table` �^�ϐ��̏ꍇ�͕ϐ��̖��O�����̂܂܎g���܂����A���̃I�v�V�����Ŏw��� 
   -  `'Position'`: �쐬����� Figure �̑傫�� 



�Ƃ��������̂����܂����B


### Arguments


R2019b ����g���� Arguments (�ڍׁF[Argument Validation Functions](https://jp.mathworks.com/help/matlab/matlab_prog/argument-validation-functions.html)) ���g���āA����Ȋ����ŃI�v�V�����̈ꗗ��\�������悤�ɂ��Ă�̂ŁA�I�v�V�����I���������y�ɂȂ��Ă���ł��傤���H




![image_2.png](barChartRaceExample_part2JP_images/image_2.png)




`barChartRace.m` �̖`���ɂ��� 


```matlab
arguments
    inputs {mustBeNumericTableTimetable(inputs)}
    options.Time (:,1) {mustBeTimeInput(options.Time,inputs)} = setDefaultTime(inputs)
    options.LabelNames {mustBeVariableLabels(options.LabelNames,inputs)} = setDefaultLabels(inputs)
    options.ColorGroups {mustBeVariableLabels(options.ColorGroups,inputs)} = setDefaultLabels(inputs)
    (����)
```


�������Ή����܂��B�ԗ�����̂͌��\��ςł������A�����ƈӐ}�����ϐ������͂���Ă��邩�ǂ����̃`�F�b�N������悤�ɂ��Ă܂��B�Ⴆ�΁E�E


```matlab
barChartRace('�G���[���o���')
```
```
�G���[: barChartRace
�ʒu 1 �̓��͈����������ł��B Input data must be either timetable, table, or numeric array (double)
```


1�ڂ̓��͂� timetable �^�� time �^�� double �̔z��ł��肢���܂��Ƃ��A


```matlab
barChartRace(T,'LabelNames',"������ǂ��Ȃ���")
```
```
�G���[: barChartRace
���O�ƒl�̈��� 'LabelNames' �������ł��B The size must be same as the number of variables of inputs (46)
```


`'LabelName'` �Ƃ����I�v�V������ input �Ɠ����ϐ��̐� (46��) �p�ӂ��Ă˂Ƃ��A�G���[�̌�����\�������銴���B�����Ŏg���֐��Ȃ�K�v�Ȃ���������܂��񂪁A���̐l�ɂ��g���Ă��炤�Ȃ炠�����ق����֗����ȂƎv������܂����B


  
# �`��̃|�C���g�P�F�f�[�^�̓��}


�e�_�����ʓ���ւ�������󋵂�\������ɂ͏��ʃf�[�^�̓��}���K�v�ł��B`barChartBar.m` �̒��ł�


```matlab
%% Interpolation: Generate nInterp data point in between
time2plot = linspace(time(1),time(end),length(time)*NumInterp);
ranking2plot = interp1(time,rankings,time2plot,Method);
data2plot = interp1(time,data,time2plot,Method);
```


����Ȋ����B`interp1` �֐��g���Ă��܂��B




������ `Method` �œ��}���@���w�肷���ł����A�V���v���ɐ��`���}����Ə�̂悤�ȓ���B������ `spline` ��ԂȂ񂩂��Ă��܂��ƁA�_�̈ʒu���I�[�o�[�V���[�g����_�C�i�~�b�N���������܂��B����܂���ˁi�΁j




![image_3.png](barChartRaceExample_part2JP_images/image_3.gif)




�R�}���h�͂���Ȋ����F`'Method'` �� `'spline'` ���w�肵�܂��B


```matlab
barChartRace(T,'NumDisplay',6,'NumInterp',4,...
    'Position',[500 60 470 370],'ColorGroups',repmat("g",length(names),1),...
    'XlabelName',"���6�s���{���̐l���i��l�j",'Method','spline',...
    'GenerateGIF',true,"Outputfilename",'top5Spline.gif');
```
# �`��̃|�C���g�Q�FCData


�O��� nonlinopt ����ɂ��w�E�������ʂ�e�_�̐F�� `CData` �v���p�e�B�Ŏw��ł��܂��B`'FaceColor'` �� `'flat'` �ɐݒ肷�邱�Ƃɂ����ӁB




�����Ȏ҂Ȃ̂� CData ���̐F�̏��Ԃ͊e�_�̈ʒu�ƘA�����Ă��܂��Ă��邱�ƁB�Ⴆ�� `CData` �����̂܂܂ɂ��Ă����ƁA���Ƃ��Ƃ̏��ʁi1 �ʁF�Ԃ� 2 �ʁF�j���t�]����ƁA1 �ʂ��� 2 �ʂ��ԂɂȂ����Ⴂ�܂��B




�Ⴆ��


```matlab
hb = barh([1,2],'FaceColor','flat');
hb.CData = [0,0,1
    1,0,0];
```

![figure_0.png](barChartRaceExample_part2JP_images/figure_0.png)



���Ƃ��Ƃ̐ݒ�ł͏オ�ԁA�����ł����A���̈ʒu��ύX����ƁE�E


```matlab
hb.XData = [2,1];
```

![figure_1.png](barChartRaceExample_part2JP_images/figure_1.png)



�F�̏��Ԃ����̂܂܁B�܂��A�A���R�ƌ����Γ��R�ȋC�����܂����B�ł��̂ŁA�ЂƎ�ԉ����� `CData` ���̏��Ԃ����킹�ĕύX����K�v������܂��B`barChartBar.m` �̒��ł�


```matlab
    % Set YTick position by ranking
    % Set YTickLabel with variable names
    [ytickpos,idx] = sort(ranking,'ascend');
    handle_axes.YTick = ytickpos;
    handle_axes.YTickLabel = LabelNames(idx);
    
    % Fix CData
    handle_bar.CData = colorScheme(idx,:);
```


�Ƃ����������� `YTick` �̏��ʕύX�ɍ��킹�� `CData` �����߂ĕύX���Ă��܂��B


# �`��̃|�C���g�R�F�_�̉��̐��l�\��


����� `text` �I�u�W�F�N�g���g���Ă��܂��B������̋L���i[MATLAB�̃v���b�g�ŃA�m�e�[�V����������](https://qiita.com/Monzo_N/items/c68f52e88fd532671a19)�j�̃R�����g�ł�����肪����܂����A`text` �I�u�W�F�N�g�̂����Ƃ���́A�v���b�g���Ă���f�[�^�Ɠ������W�n�ňʒu�w�肪�ł��邱�ƁBFigure ���̑��ΓI�ʒu�Ƃ��AAxes ���̑��ΓI�ʒu���v�Z����K�v���Ȃ��̂́A�����I�Ɏg���₷���ł��B`barChartRace.m` ���ł͋ߊ����B


```matlab
% Add value string next to the bar
if IsInteger
    displayText = string(round(value2plot(idx)));
else
    displayText = string(value2plot(idx));
end
xTextPosition = value2plot(idx) + maxValue*0.05;
yTextPosition = ytickpos;

% NumDisplay values are used
xTextPosition = xTextPosition(1:NumDisplay);
yTextPosition = yTextPosition(1:NumDisplay);
displayText = displayText(1:NumDisplay);
handle_text = text(xTextPosition,yTextPosition,displayText,'FontSize',options.FontSize);
```


�ő�l�� 5\% �����e���l����E�ɂ��炵���ʒu�ɐ��l��\�����Ă��܂��B���Ƃ��Ƃ̃f�[�^�������̏ꍇ�͐����Ɋۂ߂ĕ\������I�v�V��������Ă��܂��B���}���Ă��܂��Ă���̂ł��̂܂ܕ\������ƁA�l���������_�\���ɂȂ����Ⴄ����E�E�i�����ꂵ���j


# ���܂��̃|�C���g


�\�����ꂽ�v���b�g�݂�� "Visualized by MATLAB" �ƃA�s�[�����Ђǂ�����������܂��ˁi�΁j




����� `barCharRace.m` ���ł͈ȉ��̈�s�ŏ����Ă����ł����A�ǂ����F����D���ȕ����ɕς��Ďg���Ă��������܂��B


```matlab
% Display created by MATLAB message
text(0.99,0.02,"Visualized by MATLAB",'HorizontalAlignment','right',...
    'Units','normalized','FontSize', 10,'Color',0.5*[1,1,1]);
```
# �܂Ƃ�


�ȏ�A�ȒP�ł͂���܂��� `barChartRace` �֐����ł̃|�C���g�Љ�ł����B




�l�����ځA�l�C�v���O���~���O���ꃉ���L���O�A�e��Ƃ̎������z�����L���O�A�e���̏o���������L���O�A�e��w�΍��l�����L���O�ȂǂȂǃf�[�^��������Ζʔ������ȃv���b�g���ł������ȋC�����܂��B




�ǂ��������Ėʔ����v���b�g�����Ă��������B`barChartRace` �֐��ō��������Ƃ���Ή����Ȃ��R�����g���������B


