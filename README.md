
# Process

A Dart package that provides an abstract interface for managing system process execution. This package allows both direct execution of system commands and the injection of custom implementations, making it ideal for extensibility and unit testing.

## ✨ Features

- Abstract interface for executing system processes.
- Supports both `run` and `start` methods for process execution.
- Provides a singleton-like pattern for dependency injection.
- Default implementation delegates to Dart's `dart:io` `Process` class.
- Easily mockable for testing environments.

---

## 📦 Installation

Add the following to your `pubspec.yaml`:

```yaml
dependencies:
  process: <latest_version>
````

Then run:

```sh
dart pub get
```

---

## 🚀 Usage

### Import the package

```dart
import 'process/process.dart';
```

### Use the default implementation

```dart
void main() async {
  final result = await Process.instance.run(
    'echo',
    ['Hello, World!'],
    runInShell: true,
  );

  print('Exit code: ${result.exitCode}');
  print('Stdout: ${result.stdout}');
}
```

### Inject a custom implementation (e.g., for testing)

```dart
class MockProcess extends Process {
  @override
  Future<io.Process> start(
    String executable,
    List<String> arguments, {
    String? workingDirectory,
    bool runInShell = false,
  }) async {
    // Return a fake process or mock behavior
    throw UnimplementedError();
  }

  @override
  Future<io.ProcessResult> run(
    String executable,
    List<String> arguments, {
    bool runInShell = false,
  }) async {
    return io.ProcessResult(0, 0, 'Mocked output', '');
  }
}

void main() async {
  Process.instance = MockProcess();

  final result = await Process.instance.run('any', []);
  print('Mocked stdout: ${result.stdout}');
}
```

---

## 📄 API

### `Process.run(...)`

Runs a process and waits for its result.

### `Process.start(...)`

Starts a process asynchronously and returns the `Process` instance.

---

## 🧪 Testing

You can easily inject a mock `Process` implementation for unit testing your logic without executing real commands on the host machine.

---

## 📂 Structure

* `Process` (abstract interface)
* `_ProcessImpl` (default implementation using `dart:io`)

---

## 📜 License

[MIT](LICENSE)

---

## 💡 Contributions

Contributions are welcome! Please feel free to submit a pull request or open an issue.

