# Full part-of-speech tags in Merlin labels

You can use Festival with scripts in [Merlin](https://github.com/CSTR-Edinburgh/merlin) to create rich-context label files for TTS systems. Install Festival following [these guidelines](https://github.com/oliverwatts/ophelia/blob/master/README.md#data-preparation-1-installing-festival), and point to the installation directory with variable `$FESTDIR`. Then:


```
git clone https://github.com/CSTR-Edinburgh/merlin.git
mkdir -p /tmp/test/{txt,utt,scm,misc}
echo this is a test > /tmp/test/txt/utt1.txt
python ./merlin/misc/scripts/frontend/utils/genScmFile.py /tmp/test/txt/ /tmp/test/utt/ /tmp/test/scm/make.utts /tmp/test/misc/flist.txt
$FESTDIR/festival/bin/festival -b /tmp/test/scm/make.utts
./merlin/misc/scripts/frontend/festival_utt_to_lab/make_labels /tmp/test/lab/ /tmp/test/utt/ $FESTDIR/festival/examples/dumpfeats ./merlin/misc/scripts/frontend/festival_utt_to_lab/
```

This will create a fullcontext label file under `/tmp/test/lab/full/utt1.lab` which looks like:

```
        0    1500000 x^x-pau+dh=ih@x_x/A:0_0_0/B:x-x-x@x-x&x-x#x-x$x-x!x-x;x-x|x/C:1+0+3/D:0_0/E:x+x@x+x&x+x#x+x/F:det_1/G:0_0/H:x=x@1=1|0/I:4=4/J:4+4-1
   1500000    1995180 x^pau-dh+ih=s@1_3/A:0_0_0/B:1-0-3@1-1&1-4#1-3$1-2!0-1;0-3|ih/C:1+0+2/D:0_0/E:det+1@1+4&1+1#0+3/F:aux_1/G:0_0/H:4=4@1=1|L-L%/I:0=0/J:4+4-1
   1995180    2744600 pau^dh-ih+s=ih@2_2/A:0_0_0/B:1-0-3@1-1&1-4#1-3$1-2!0-1;0-3|ih/C:1+0+2/D:0_0/E:det+1@1+4&1+1#0+3/F:aux_1/G:0_0/H:4=4@1=1|L-L%/I:0=0/J:4+4-1
   2744600    3745140 dh^ih-s+ih=z@3_1/A:0_0_0/B:1-0-3@1-1&1-4#1-3$1-2!0-1;0-3|ih/C:1+0+2/D:0_0/E:det+1@1+4&1+1#0+3/F:aux_1/G:0_0/H:4=4@1=1|L-L%/I:0=0/J:4+4-1
   3745140    4238200 ih^s-ih+z=ax@1_2/A:1_0_3/B:1-0-2@1-1&2-3#1-2$1-2!1-2;0-2|ih/C:0+0+1/D:det_1/E:aux+1@2+3&1+1#0+2/F:det_1/G:0_0/H:4=4@1=1|L-L%/I:0=0/J:4+4-1
   4238200    4950570 s^ih-z+ax=t@2_1/A:1_0_3/B:1-0-2@1-1&2-3#1-2$1-2!1-2;0-2|ih/C:0+0+1/D:det_1/E:aux+1@2+3&1+1#0+2/F:det_1/G:0_0/H:4=4@1=1|L-L%/I:0=0/J:4+4-1
   4950570    5395500 ih^z-ax+t=eh@1_1/A:1_0_2/B:0-0-1@1-1&3-2#2-2$1-2!1-1;0-1|ax/C:1+1+4/D:aux_1/E:det+1@3+2&1+1#0+1/F:content_1/G:0_0/H:4=4@1=1|L-L%/I:0=0/J:4+4-1
   5395500    6452180 z^ax-t+eh=s@1_4/A:0_0_1/B:1-1-4@1-1&4-1#2-1$1-1!2-0;0-0|eh/C:0+0+0/D:det_1/E:content+1@4+1&1+0#0+0/F:0_0/G:0_0/H:4=4@1=1|L-L%/I:0=0/J:4+4-1
   6452180    8056480 ax^t-eh+s=t@2_3/A:0_0_1/B:1-1-4@1-1&4-1#2-1$1-1!2-0;0-0|eh/C:0+0+0/D:det_1/E:content+1@4+1&1+0#0+0/F:0_0/G:0_0/H:4=4@1=1|L-L%/I:0=0/J:4+4-1
   8056480    9679410 t^eh-s+t=pau@3_2/A:0_0_1/B:1-1-4@1-1&4-1#2-1$1-1!2-0;0-0|eh/C:0+0+0/D:det_1/E:content+1@4+1&1+0#0+0/F:0_0/G:0_0/H:4=4@1=1|L-L%/I:0=0/J:4+4-1
   9679410   10307600 eh^s-t+pau=x@4_1/A:0_0_1/B:1-1-4@1-1&4-1#2-1$1-1!2-0;0-0|eh/C:0+0+0/D:det_1/E:content+1@4+1&1+0#0+0/F:0_0/G:0_0/H:4=4@1=1|L-L%/I:0=0/J:4+4-1
  10307600   11807600 s^t-pau+x=x@x_x/A:1_1_4/B:x-x-x@x-x&x-x#x-x$x-x!x-x;x-x|x/C:0+0+0/D:content_1/E:x+x@x+x&x+x#x+x/F:0_0/G:4_4/H:x=x@1=1|0/I:0=0/J:4+4-1
```

The string after `E:` indicates the "guess part of speech" (gpos) of the current word. See the definition of Word.gpos in the [Festival documentation](http://www.cstr.ed.ac.uk/projects/festival/manual/festival_32.html).

To get Festival's full part of speech tags, modify the definition of the features to be extracted from Festival utterances:

```
sed -i 's/gpos/pos/g' ./merlin/misc/scripts/frontend/festival_utt_to_lab/label.feats
```

Then run the last part again writing to a new directory:

```
mkdir /tmp/test/lab2/
./merlin/misc/scripts/frontend/festival_utt_to_lab/make_labels /tmp/test/lab2/ /tmp/test/utt/ $FESTDIR/festival/examples/dumpfeats ./merlin/misc/scripts/frontend/festival_utt_to_lab/
```

See the output:

```
         0    1500000 x^x-pau+dh=ih@x_x/A:0_0_0/B:x-x-x@x-x&x-x#x-x$x-x!x-x;x-x|x/C:1+0+3/D:0_0/E:x+x@x+x&x+x#x+x/F:dt_1/G:0_0/H:x=x@1=1|0/I:4=4/J:4+4-1
   1500000    1995180 x^pau-dh+ih=s@1_3/A:0_0_0/B:1-0-3@1-1&1-4#1-3$1-2!0-1;0-3|ih/C:1+0+2/D:0_0/E:dt+1@1+4&1+1#0+3/F:vbz_1/G:0_0/H:4=4@1=1|L-L%/I:0=0/J:4+4-1
   1995180    2744600 pau^dh-ih+s=ih@2_2/A:0_0_0/B:1-0-3@1-1&1-4#1-3$1-2!0-1;0-3|ih/C:1+0+2/D:0_0/E:dt+1@1+4&1+1#0+3/F:vbz_1/G:0_0/H:4=4@1=1|L-L%/I:0=0/J:4+4-1
   2744600    3745140 dh^ih-s+ih=z@3_1/A:0_0_0/B:1-0-3@1-1&1-4#1-3$1-2!0-1;0-3|ih/C:1+0+2/D:0_0/E:dt+1@1+4&1+1#0+3/F:vbz_1/G:0_0/H:4=4@1=1|L-L%/I:0=0/J:4+4-1
   3745140    4238200 ih^s-ih+z=ax@1_2/A:1_0_3/B:1-0-2@1-1&2-3#1-2$1-2!1-2;0-2|ih/C:0+0+1/D:dt_1/E:vbz+1@2+3&1+1#0+2/F:dt_1/G:0_0/H:4=4@1=1|L-L%/I:0=0/J:4+4-1
   4238200    4950570 s^ih-z+ax=t@2_1/A:1_0_3/B:1-0-2@1-1&2-3#1-2$1-2!1-2;0-2|ih/C:0+0+1/D:dt_1/E:vbz+1@2+3&1+1#0+2/F:dt_1/G:0_0/H:4=4@1=1|L-L%/I:0=0/J:4+4-1
   4950570    5395500 ih^z-ax+t=eh@1_1/A:1_0_2/B:0-0-1@1-1&3-2#2-2$1-2!1-1;0-1|ax/C:1+1+4/D:vbz_1/E:dt+1@3+2&1+1#0+1/F:nn_1/G:0_0/H:4=4@1=1|L-L%/I:0=0/J:4+4-1
   5395500    6452180 z^ax-t+eh=s@1_4/A:0_0_1/B:1-1-4@1-1&4-1#2-1$1-1!2-0;0-0|eh/C:0+0+0/D:dt_1/E:nn+1@4+1&1+0#0+0/F:0_0/G:0_0/H:4=4@1=1|L-L%/I:0=0/J:4+4-1
   6452180    8056480 ax^t-eh+s=t@2_3/A:0_0_1/B:1-1-4@1-1&4-1#2-1$1-1!2-0;0-0|eh/C:0+0+0/D:dt_1/E:nn+1@4+1&1+0#0+0/F:0_0/G:0_0/H:4=4@1=1|L-L%/I:0=0/J:4+4-1
   8056480    9679410 t^eh-s+t=pau@3_2/A:0_0_1/B:1-1-4@1-1&4-1#2-1$1-1!2-0;0-0|eh/C:0+0+0/D:dt_1/E:nn+1@4+1&1+0#0+0/F:0_0/G:0_0/H:4=4@1=1|L-L%/I:0=0/J:4+4-1
   9679410   10307600 eh^s-t+pau=x@4_1/A:0_0_1/B:1-1-4@1-1&4-1#2-1$1-1!2-0;0-0|eh/C:0+0+0/D:dt_1/E:nn+1@4+1&1+0#0+0/F:0_0/G:0_0/H:4=4@1=1|L-L%/I:0=0/J:4+4-1
  10307600   11807600 s^t-pau+x=x@x_x/A:1_1_4/B:x-x-x@x-x&x-x#x-x$x-x!x-x;x-x|x/C:0+0+0/D:nn_1/E:x+x@x+x&x+x#x+x/F:0_0/G:4_4/H:x=x@1=1|0/I:0=0/J:4+4-1
```

Note how the POS of the word "test" is now "nn" (noun) rather than "content" as previously.



