# HTS_prog_1

<?php

function unscrambleWords($scrambledWords, $wordList) {
    $unscrambledWords = [];
    $scrambledWords = explode(',', $scrambledWords);

    foreach ($scrambledWords as $scrambledWord) {
        $scrambledWord = trim($scrambledWord); 
        $sortedScrambledWord = sortCharacters($scrambledWord);

       
        foreach ($wordList as $word) {
            $sortedWord = sortCharacters($word);
            if ($sortedWord === $sortedScrambledWord) {
                $unscrambledWords[$scrambledWord][] = $word;
            }
        }
    }

    return $unscrambledWords;
}

function sortCharacters($word) {
    $characters = str_split($word);
    sort($characters);
    return implode('', $characters);
}

// siia copy-paste scrambled sõnad:
$scrambledWords = "
aildsn,
evblloy,
dobrtge,
cseryiut,
oetsiot,
aowesme,
rnbida,
wreeusn,
myckie,
ceonil ";
$wordListFile = "wordlist.txt"; 


$wordList = file($wordListFile, FILE_IGNORE_NEW_LINES | FILE_SKIP_EMPTY_LINES);

$unscrambledWords = unscrambleWords($scrambledWords, $wordList);

foreach ($unscrambledWords as $scrambledWord => $words) {
    if (!empty($words)) {
        echo implode($words) . ", ";
    }
}
