object-monitor
==============

A simple library containing interfaces for generic object monitoring. For now I have implemented filesystem monitoring based on inotify. Similary one can also implement monitoring for other resources for example socket etc.

Example
========
```
#include <iostream>
#include <sys/inotify.h>
#include <glog/logging.h>

#include "system/monitor/fileWatcher.hpp"
#include "system/core/file.hpp"

using namespace std;
using namespace mkTest;
using namespace mkTest::system;

int main(int argc, const char*argv[])
{
  std::shared_ptr<File> file(new File("/home"));
  std::shared_ptr<FileWatcherImpl> fimpl(new FileWatcherImpl);

  std::shared_ptr<FileWatcher> fw (new FileWatcher(file, IN_ALL_EVENTS));
  fw->setImpl(fimpl);

  fw->start();
  for (;;) {
    fw->update();
  }
  
  return 0;
}
```
