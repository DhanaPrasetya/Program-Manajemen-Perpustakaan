#include <iostream>
#include <limits>

using namespace std;

struct TreeNode { // Define tree
    int idNumber;
    string bookName;
    string description;
    string genre;
    TreeNode* left;
    TreeNode* right;

    TreeNode(int id, string name, string descr, string gen) : idNumber(id), bookName(name),
    description(descr), genre(gen), left(nullptr), right(nullptr) {} // Initialize
};

TreeNode* insert(TreeNode* root, int idNumber1, string bookName1, string description1, string genre1) { // Insert new node

    if (root == nullptr) {
        return new TreeNode(idNumber1, bookName1, description1, genre1); // If tree empty, create node as a root
    }

    if (idNumber1 < root->idNumber) {
        root->left = insert(root->left, idNumber1, bookName1, description1, genre1); // Insert in the left subtree

    } else {
        root->right = insert(root->right, idNumber1, bookName1, description1, genre1); // Insert in the right subtree
    }

    return root;
}

TreeNode* findMin(TreeNode* node) {
    while (node->left != nullptr) {
        node = node->left;
    }
    return node;
}

TreeNode* removeBook(TreeNode* root, int idNumber) {
    if (root == nullptr) { // If empty, return (cancell)
        return root;
    }

    if (idNumber < root->idNumber) {
        root->left = removeBook(root->left, idNumber);

    } else if (idNumber > root->idNumber) {
        root->right = removeBook(root->right, idNumber);

    } else {

        if (root->left == nullptr) { // If no left child, return to right child
            TreeNode* temp = root->right;
            delete root;
            return temp;

        } else if (root->right == nullptr) { // If no right child, return to left child
            TreeNode* temp = root->left;
            delete root;
            return temp;
        }

        TreeNode* temp = findMin(root->right);
        root->idNumber = temp->idNumber;
        root->bookName = temp->bookName;
        root->description = temp->description;
        root->genre = temp->genre;
        root->right = removeBook(root->right, temp->idNumber);
    }
    return root;
}


void inOrderTraversal(TreeNode* root) { // Print tree node in order tranversal method

    if (root == nullptr) {
        return;
    }

    inOrderTraversal(root->left);

    cout << "\n--------------------------\n";
    cout << "ID buku        = " << root->idNumber << endl;
    cout << "Nama Buku      = " << root->bookName << endl;
    cout << "Deskripsi buku = " << root->description << endl;
    cout << "Genre Buku     = " << root->genre << endl;

    inOrderTraversal(root->right);
}

void failInput(int &input) { 

    while (true) {

        if (cin.fail()) {
            cin.clear();
            cin.ignore(numeric_limits<streamsize>::max(), '\n'); // If input not integer, repeat
            cout << "\n>> Input bukan huruf\n\n";
            cout << "> ";
            cin >> input;

        } else {
            cin.ignore(numeric_limits<streamsize>::max(), '\n');
            break;
        }
    }
}


TreeNode* searchId(TreeNode* root, int id) { // Search node by ID
    if (root == nullptr || root->idNumber == id) {
        return root;
    }

    if (id < root->idNumber) {
        return searchId(root->left, id);
    } else {
        return searchId(root->right, id);
    }
}

int idNumber(const string& bookName) { // Generate ID by book name
    int resultASCII = 0;

    for (char ch : bookName) {
        if (ch != ' ') {
            resultASCII += (tolower(ch) - 'a' + 1);
        }
    }

    return resultASCII;
}

int main() {

    TreeNode* root = nullptr;

    cout << "---------------Program Manajemen Perpustakaan---------------\n";
    cout << "\n";

    do {
        int path;

        cout << "\n------------------------------------\n";
        cout << "0. Keluar dari program\n";
        cout << "1. Tampilkan data buku yang tersedia\n";
        cout << "2. Cari buku berdasarkan ID\n";
        cout << "3. Tambahkan buku\n";
        cout << "4. Hapus buku\n";
        cout << "------------------------------------\n";
        cout << "> ";

        cin >> path;

        failInput(path); // Handling fail input

        if (path == 0) {
            cout << "\n>> Keluar dari program\n";
            break;

        } else if (path == 1) {

            if (root == nullptr) {
                cout << "\n>> Tidak ada buku yang tersimpan!\n";
            } else {
                inOrderTraversal(root);
            }

        } else if (path == 2) {

            do {
                if (root == nullptr) {
                    cout << "\n>> Tidak ada buku yang tersimpan!\n";
                    break;
                }

                int idInput;

                cout << "\n2.1 Masukkan ID buku yang ingin dicari (masukkan '0' untuk kembali ke menu utama)\n";
                cout << "> ";
                cin >> idInput;

                failInput(idInput);

                cout << "\n";

                if (idInput == 0) {
                    cout << "\n>> Kembali ke menu utama\n\n";
                    break;
                }

                TreeNode* result = searchId(root, idInput); // Search tree based on book ID

                if (result != nullptr) {
                    cout << "2.2 Buku dengan ID " << idInput << " adalah berikut\n";
                    cout << "------------------------------------------\n";
                    cout << "Nama Buku  = " << result->bookName << endl;
                    cout << "Deskripsi  = " << result->description << endl;
                    cout << "Genre      = " << result->genre << endl;
                    cout << "------------------------------------------\n";
                    
                } else {
                    cout << ">> Buku dengan ID " << idInput << " tidak ditemukan!" << endl;
                }

            } while(true);

        } else if (path == 3) {

            do {
                string addBookName;
                string addBookDescription;
                string addBookGenre;
                int genre;
                int id;

                do {
                    cout << "\n3.1 Masukkan judul buku (masukkan '0' untuk membatalkan dan kembali ke menu utama)\n";
                    cout << "> ";
                    getline(cin, addBookName);

                    if (addBookName == "0") {
                        break;
                    }

                    id = idNumber(addBookName); // Generate book ID
                    TreeNode* result = searchId(root, id);

                    while (result != nullptr && result->bookName != addBookName) { // Collision handling based on book ID
                        id += id;
                        result = searchId(root, id);
                    }

                    if (result != nullptr && result->bookName == addBookName) { // Checking book name, if already exist == reject
                        cout << "3.4 Buku dengan judul '" << addBookName << "' sudah tersedia!\n";

                    } else {
                        break;
                    }

                } while (true);

                if (addBookName == "0") { // Back to main menu
                    cout << "\n>> Kembali ke menu utama\n";
                    break;
                }

                cout << "\n3.2 Masukkan deskripsi buku (masukkan '0' untuk membatalkan dan kembali ke menu utama)\n";
                cout << "> ";
                getline(cin, addBookDescription);
                if (addBookDescription == "0") {
                    cout << "\n>> Kembali ke menu utama\n";
                    break;
                }

                cout << "\n3.3 Masukkan genre (masukkan '0' untuk membatalkan dan kembali ke menu utama)";
                cout << "\nMasukkan '1' untuk buku non-fiksi\n";
                cout << "Masukkan '2' untuk buku fiksi\n";
                cout << "> ";

                do {
                    cin >> genre;

                    failInput(genre); // Handling fail input

                    if (genre == 0) {
                        cout << "\n>> Kembali ke menu utama\n"; // Back to main menu
                        break;

                    } else if (genre == 1) {
                        addBookGenre = "Non-fiksi";
                        break;

                    } else if (genre == 2) {
                        addBookGenre = "Fiksi";
                        break;

                    } else {
                        cout << "\n>> Input invalid, mohon diulangi\n";
                        cout << "> ";
                    }

                } while (true);

                if (genre == 0) { // Back to main menu
                    break;
                }

                root = insert(root, id, addBookName, addBookDescription, addBookGenre); // Insert data to tree
                cout << "\n>> Buku berhasil ditambahkan!\n";

            } while (true);

        } else if (path == 4){

            do {

                int idInput;

                cout << "\n4.1 Masukkan ID buku yang ingin dihapus (masukkan '0' untuk kembali ke menu utama)\n";
                cout << "> ";
                cin >> idInput;

                failInput(idInput);

                if (root == nullptr) {
                    cout << "\n>> Tidak ada buku yang tersimpan!\n";
                    break;
                }

                cout << "\n";

                if (idInput == 0) {
                    cout << "\n>> Kembali ke menu utama\n\n";
                    break;
                }

                TreeNode* result = searchId(root, idInput); // Search tree based on book ID

                if (result != nullptr) {
                    int choice;
                    string bookNameDeleted = result->bookName;

                    cout << "4.2 Buku dengan ID " << idInput << " adalah berikut\n";
                    cout << "------------------------------------------\n";
                    cout << "Nama Buku  = " << result->bookName << endl;
                    cout << "Deskripsi  = " << result->description << endl;
                    cout << "Genre      = " << result->genre << endl;
                    cout << "------------------------------------------\n";

                    cout << "\nApakah anda yakin ingin menghapus buku berjudul '"<< bookNameDeleted <<"'?\n";
                    cout << "Masukkan '1' untuk menghapus buku\n";
                    cout << "Masukkan '2' untuk membatalkan\n";
                    cout << "> ";

                    do {

                        cin >> choice;
                        failInput(choice);

                        if (choice == 1) {
                            root = removeBook(root, idInput);
                            cout << "\n>> Buku berjudul '" << bookNameDeleted << "' telah dihapus!\n";
                            break;

                        } else if (choice == 2) {
                            cout << "\n>> Penghapusan buku dibatalkan\n";
                            break;
                        
                        } else {
                            cout << "\n>> Input invalid, mohon diulangi\n";
                            cout << "> ";
                        }

                    } while(true);
                    
                } else {
                    cout << ">> Buku dengan ID " << idInput << " tidak ditemukan!" << endl;
                }

            } while(true);


        } else if (path < 0){
            cout << "\n>> Input bukan bilangan negatif\n";
        
        } else {
            cout << "\n>> Input terlalu besar\n";
        }

    } while (true);

    return 0;
}
