<?php
function generateFilename($title, $author) {
    $timestamp = date("YmdHis");
    $title = strtolower(preg_replace("/[^a-zA-Z0-9]+/", "-", $title));
    $author = strtolower(preg_replace("/[^a-zA-Z0-9]+/", "-", $author));
    return $title . "-" . $author . "-" . $timestamp . ".md";
}

function promptInput($prompt) {
    echo $prompt . ": ";
    return trim(fgets(STDIN));
}

$title = promptInput("Enter the blog post title");
$author = promptInput("Enter the author's name");
$category = promptInput("Enter the category");

if ($argc >= 2) {
    $outputDir = $argv[1];
} else {
    $outputDir = getcwd();
}

$filename = generateFilename($title, $author);
$filepath = $outputDir . "/" . $filename;

$date = date("Y-m-d");
$content = <<<EOD
---
title: "$title"
author: "$author"
category: "$category"
date: "$date"
---

Write your blog post content here...
EOD;

file_put_contents($filepath, $content);

echo "Blog post template generated successfully at: $filepath\n";
?>

# php
