#include <iostream>
#include <fstream>
#include <string>
using namespace std;

// Run-Length Encoding (RLE) Compression
string compress(const string& input) {
    string result;
    int count = 1;
    for (size_t i = 1; i <= input.size(); i++) {
        if (i < input.size() && input[i] == input[i - 1]) {
            count++;
        } else {
            result += input[i - 1];
            result += to_string(count);
            count = 1;
        }
    }
    return result;
}

// Run-Length Encoding (RLE) Decompression
string decompress(const string& input) {
    string result;
    for (size_t i = 0; i < input.size(); i += 2) {
        char c = input[i];
        int count = input[i + 1] - '0';
        result.append(count, c);
    }
    return result;
}

int main() {
    string text;
    cout << "Enter text to compress: ";
    cin >> text;

    string compressed = compress(text);
    string decompressed = decompress(compressed);

    cout << "Compressed: " << compressed << endl;
    cout << "Decompressed: " << decompressed << endl;

    return 0;
}
