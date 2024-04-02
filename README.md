<?php
// Отримання введених даних від користувача
echo "Введіть назву публікації в блозі: ";
$title = readline();
echo "Введіть ім'я автора: ";
$author = readline();
echo "Введіть категорію(ї): ";
$category = readline();

// Перевірка чи вказано вихідний каталог через аргумент командного рядка
$outputDirectory = isset($argv[1]) ? $argv[1] : getcwd();

// Перевірка та створення необхідних каталогів
if (!file_exists($outputDirectory)) {
    mkdir($outputDirectory, 0777, true);
}

// Генерація унікальної назви файлу
$timestamp = date('YmdHis');
$filename = sprintf('%s-%s-%s.md', strtolower(str_replace(' ', '-', $title)), strtolower(str_replace(' ', '-', $author)), $timestamp);

// Створення та запис шаблону публікації блогу
$content = <<<EOT
---
назва: "{$title}"
автор: "{$author}"
категорія: "{$category}"
дата: "{$timestamp}"
---

Напишіть вміст свого блогу тут...
EOT;

// Запис шаблону у файл розмітки
file_put_contents($outputDirectory . '/' . $filename, $content);

// Вивід шляху до файлу для користувача
echo "Файл успішно згенеровано за шляхом: " . $outputDirectory . '/' . $filename . "\n";
?>

