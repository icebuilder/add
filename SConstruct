import os

VariantDir('build', 'src')
GTEST_INCLUDE = 'include'

testEnv = Environment(
	ENV = os.environ,
	CCFLAGS = '-ggdb -Wall -I %s' % (GTEST_INCLUDE),
	CFLAGS = '-fprofile-arcs -ftest-coverage',
	LINKFLAGS = '-fprofile-arcs -ftest-coverage',
	LIBPATH = 'library',
	LIBS = ['pthread', 'libgtest']
)

sources = ['build/add.c']
testSources = ['build/add_test.cc']

testProg = testEnv.Program('a.out', sources + testSources)
testReport = testEnv.Command('test_report.xml', testProg,
	"./a.out --gtest_output=xml:${TARGET}")
coverageReport = testEnv.Command('coverage.xml', testReport,
	"./bin/gcovr -x -r build -o ${TARGET}")

Default(coverageReport)
