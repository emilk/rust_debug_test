This is a minimal Rust repository to reproduce a problem I'm having with debugging in VS Code using the CodeLLDB extension.

When attempting to run the debugger I get "process resume at entry point failed: Resume timed out.". Turning on verbose logging in the CodeLLDB extension I see this in the `Output` tab:

```
Running `cargo build --bin=rust_debug_test --package=rust_debug_test --message-format=json`...
    Finished dev [unoptimized + debuginfo] target(s) in 0.03s
Raw artifacts:
{
  fileName: '/Users/emilk/code/rust_debug_test/target/debug/rust_debug_test',
  name: 'rust_debug_test',
  kind: 'bin'
}
Filtered artifacts:
{
  fileName: '/Users/emilk/code/rust_debug_test/target/debug/rust_debug_test',
  name: 'rust_debug_test',
  kind: 'bin'
}
configuration: {
  type: 'lldb',
  request: 'launch',
  name: "Debug executable 'rust_debug_test'",
  args: [],
  cwd: '${workspaceFolder}',
  __configurationTarget: 5,
  relativePathBase: '/Users/emilk/code/rust_debug_test',
  program: '/Users/emilk/code/rust_debug_test/target/debug/rust_debug_test',
  sourceLanguages: [ 'rust' ]
}
liblldb: /Users/emilk/.vscode/extensions/vadimcn.vscode-lldb-1.6.10/lldb/lib/liblldb.dylib
environment: {}
params: {
  evaluateForHovers: true,
  commandCompletions: true,
  sourceLanguages: [ 'rust' ]
}
Listening on port 62938
[2022-03-09T13:34:19.051Z DEBUG codelldb] New debug session
INFO(Python) 14:34:19 formatters: Initializing
INFO(Python) 14:34:19 formatters.rust: Initializing
[2022-03-09T13:34:19.427Z DEBUG codelldb::dap_codec] --> {"command":"initialize","arguments":{"clientID":"vscode","clientName":"Visual Studio Code","adapterID":"lldb","pathFormat":"path","linesStartAt1":true,"columnsStartAt1":true,"supportsVariableType":true,"supportsVariablePaging":true,"supportsRunInTerminalRequest":true,"locale":"en-us","supportsProgressReporting":true,"supportsInvalidatedEvent":true,"supportsMemoryReferences":true},"type":"request","seq":1}
[2022-03-09T13:34:19.433Z DEBUG codelldb::dap_codec] <-- {"type":"response","request_seq":1,"success":true,"command":"initialize","body":{"exceptionBreakpointFilters":[{"default":true,"filter":"rust_panic","label":"Rust: on panic"}],"supportTerminateDebuggee":true,"supportsCancelRequest":true,"supportsCompletionsRequest":true,"supportsConditionalBreakpoints":true,"supportsConfigurationDoneRequest":true,"supportsDataBreakpoints":true,"supportsDelayedStackTraceLoading":true,"supportsEvaluateForHovers":true,"supportsFunctionBreakpoints":true,"supportsGotoTargetsRequest":true,"supportsHitConditionalBreakpoints":true,"supportsLogPoints":true,"supportsReadMemoryRequest":true,"supportsRestartFrame":true,"supportsSetVariable":true}}
[2022-03-09T13:34:19.438Z DEBUG codelldb::dap_codec] --> {"command":"launch","arguments":{"type":"lldb","request":"launch","name":"Debug executable 'rust_debug_test'","args":[],"cwd":"/Users/emilk/code/rust_debug_test","__configurationTarget":5,"relativePathBase":"/Users/emilk/code/rust_debug_test","program":"/Users/emilk/code/rust_debug_test/target/debug/rust_debug_test","sourceLanguages":["rust"],"_adapterSettings":{"displayFormat":"auto","showDisassembly":"auto","dereferencePointers":true,"suppressMissingSourceFiles":true,"evaluationTimeout":5,"consoleMode":"commands","sourceLanguages":null,"terminalPromptClear":null,"evaluateForHovers":true,"commandCompletions":true,"reproducer":false},"__sessionId":"b726b825-a494-4038-bcab-94977064abc9"},"type":"request","seq":2}
[2022-03-09T13:34:19.441Z DEBUG codelldb::dap_codec] <-- {"type":"event","seq":1,"event":"capabilities","body":{"capabilities":{"exceptionBreakpointFilters":[{"default":true,"filter":"rust_panic","label":"Rust: on panic"}],"supportTerminateDebuggee":true,"supportsCancelRequest":true,"supportsCompletionsRequest":true,"supportsConditionalBreakpoints":true,"supportsConfigurationDoneRequest":true,"supportsDataBreakpoints":true,"supportsDelayedStackTraceLoading":true,"supportsEvaluateForHovers":true,"supportsFunctionBreakpoints":true,"supportsGotoTargetsRequest":true,"supportsHitConditionalBreakpoints":true,"supportsLogPoints":true,"supportsReadMemoryRequest":true,"supportsRestartFrame":true,"supportsSetVariable":true}}}
[2022-03-09T13:34:19.522Z DEBUG codelldb::dap_codec] <-- {"type":"event","seq":2,"event":"initialized"}
[2022-03-09T13:34:19.522Z DEBUG codelldb::debug_session] Debug event: 0x6000031f0698 Event: broadcaster = 0x7fd19c815440 (lldb.target), type = 0x00000002 (modules-loaded), data = {rust_debug_test}
[2022-03-09T13:34:19.524Z DEBUG codelldb::dap_codec] <-- {"type":"event","seq":3,"event":"module","body":{"module":{"addressRange":"FFFFFFFFFFFFFFFF","id":"FFFFFFFFFFFFFFFF","name":"rust_debug_test","path":"/Users/emilk/code/rust_debug_test/target/debug/rust_debug_test","symbolFilePath":"/Users/emilk/code/rust_debug_test/target/debug/rust_debug_test","symbolStatus":"Symbols loaded."},"reason":"new"}}
[2022-03-09T13:34:19.524Z DEBUG codelldb::dap_codec] <-- {"type":"request","seq":4,"command":"runInTerminal","arguments":{"args":["/Users/emilk/.vscode/extensions/vadimcn.vscode-lldb-1.6.10/adapter/codelldb","terminal-agent","--port=62941"],"cwd":"","kind":"integrated","title":"Debug executable 'rust_debug_test'"}}
[2022-03-09T13:34:19.526Z DEBUG codelldb::dap_codec] --> {"command":"setFunctionBreakpoints","arguments":{"breakpoints":[]},"type":"request","seq":3}
[2022-03-09T13:34:19.527Z DEBUG codelldb::dap_codec] <-- {"type":"response","request_seq":3,"success":true,"command":"setFunctionBreakpoints","body":{"breakpoints":[]}}
[2022-03-09T13:34:19.532Z DEBUG codelldb::dap_codec] --> {"command":"setDataBreakpoints","arguments":{"breakpoints":[]},"type":"request","seq":4}
[2022-03-09T13:34:19.532Z DEBUG codelldb::dap_codec] <-- {"type":"response","request_seq":4,"success":true,"command":"setDataBreakpoints","body":{"breakpoints":[]}}
[2022-03-09T13:34:19.535Z DEBUG codelldb::dap_codec] --> {"command":"setExceptionBreakpoints","arguments":{"filters":["rust_panic"]},"type":"request","seq":5}
[2022-03-09T13:34:19.564Z DEBUG codelldb::dap_codec] --> {"type":"response","seq":6,"command":"runInTerminal","request_seq":4,"success":true,"body":{"shellProcessId":72582}}
[2022-03-09T13:34:19.569Z DEBUG codelldb::debug_session] Debug event: 0x6000031e1718 Event: broadcaster = 0x7fd19c815440 (lldb.target), type = 0x00000001 (breakpoint-changed), data = {}
[2022-03-09T13:34:19.569Z DEBUG codelldb::dap_codec] <-- {"type":"response","request_seq":5,"success":true,"command":"setExceptionBreakpoints"}
[2022-03-09T13:34:19.576Z DEBUG codelldb::dap_codec] --> {"command":"configurationDone","type":"request","seq":7}
[2022-03-09T13:34:19.578Z DEBUG codelldb::dap_codec] <-- {"type":"response","request_seq":7,"success":true,"command":"configurationDone"}
[2022-03-09T13:34:19.585Z DEBUG codelldb::dap_codec] --> {"command":"threads","type":"request","seq":8}
[2022-03-09T13:34:19.585Z DEBUG codelldb::dap_codec] <-- {"type":"response","request_seq":8,"success":true,"command":"threads","body":{"threads":[]}}
[2022-03-09T13:34:19.600Z DEBUG codelldb::dap_codec] <-- {"type":"event","seq":5,"event":"output","body":{"output":"Launching: /Users/emilk/code/rust_debug_test/target/debug/rust_debug_test\n"}}
[2022-03-09T13:34:24.952Z ERROR codelldb::debug_session] process resume at entry point failed: Resume timed out.
[2022-03-09T13:34:24.952Z DEBUG codelldb::debug_session] Debug event: 0x6000031f9418 Event: broadcaster = 0x7fd19c815440 (lldb.target), type = 0x00000001 (breakpoint-changed), data = {}
[2022-03-09T13:34:24.952Z DEBUG codelldb::dap_codec] <-- {"type":"response","request_seq":2,"success":false,"command":"","message":"process resume at entry point failed: Resume timed out.","show_user":true}
[2022-03-09T13:34:24.952Z DEBUG codelldb::debug_session] Debug event: 0x6000031f9458 Event: broadcaster = 0x7fd19c815440 (lldb.target), type = 0x00000004 (modules-unloaded), data = {rust_debug_test}
[2022-03-09T13:34:24.952Z DEBUG codelldb::dap_codec] <-- {"type":"event","seq":6,"event":"module","body":{"module":{"id":"FFFFFFFFFFFFFFFF","name":""},"reason":"removed"}}
[2022-03-09T13:34:24.952Z DEBUG codelldb::debug_session] Debug event: 0x6000031fba58 Event: broadcaster = 0x7fd19c815440 (lldb.target), type = 0x00000002 (modules-loaded), data = {dyld, runtime}
[2022-03-09T13:34:24.952Z DEBUG codelldb::debug_session] Debug event: 0x600002ac7450 Event: broadcaster = 0x7fd199a18050 (lldb.process), type = 0x00000001 (state-changed), data = { process = 0x7fd199a18018 (pid = 72653), state = running}
[2022-03-09T13:34:24.953Z DEBUG codelldb::dap_codec] <-- {"type":"event","seq":7,"event":"module","body":{"module":{"addressRange":"20006C000","id":"20006C000","name":"dyld","path":"/usr/lib/dyld","symbolFilePath":"/usr/lib/dyld","symbolStatus":"Symbols loaded."},"reason":"new"}}
[2022-03-09T13:34:24.953Z DEBUG codelldb::debug_session] Debug event: 0x600002ac77e0 Event: broadcaster = 0x7fd199a18050 (lldb.process), type = 0x00000001 (state-changed), data = { process = 0x7fd199a18018 (pid = 72653), state = exited}
[2022-03-09T13:34:24.953Z DEBUG codelldb::dap_codec] <-- {"type":"event","seq":8,"event":"module","body":{"module":{"addressRange":"7FF7FFFB8000","id":"7FF7FFFB8000","name":"runtime","path":"/usr/libexec/rosetta/runtime","symbolFilePath":"/usr/libexec/rosetta/runtime","symbolStatus":"Symbols loaded."},"reason":"new"}}
thread '<unnamed>' panicked at 'Whoops! Something that was supposed to have been initialized at this point, wasn't.', [2022-03-09T13:34:24.953Z DEBUG codelldb::dap_codec] <-- {"type":"event","seq":9,"event":"continued","body":{"allThreadsContinued":true,"threadId":0}}
adapter/src/must_initialize.rs:32:17
note: run with `RUST_BACKTRACE=1` environment variable to display a backtrace
[2022-03-09T13:34:24.955Z DEBUG codelldb] Session has ended
[2022-03-09T13:34:24.968Z DEBUG codelldb] Exiting
Debug adapter exit code=0, signal=null.
```
