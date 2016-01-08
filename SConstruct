import os

VariantDir('build', 'src')
GTEST_HOME = '/home/icebuilder/local_ws/googletest-master/googletest/'
GTEST_LIB = '/home/icebuilder/local_ws/googletest-master/build/googlemock/gtest/'
GTEST_INCLUDE = os.path.join(GTEST_HOME, 'include')

testEnv = Environment(
	ENV = os.environ,
	CCFLAGS = '-ggdb -Wall -I %s' % (GTEST_INCLUDE),
	CFLAGS = '-fprofile-arcs -ftest-coverage',
	LINKFLAGS = '-fprofile-arcs -ftest-coverage',
	LIBPATH = [GTEST_LIB, GTEST_HOME],
	LIBS = ['pthread', 'libgtest']
)

sources = ['build/add.c']
testSources = ['build/add_test.cc']

testProg = testEnv.Program('a.out', sources + testSources)
testReport = testEnv.Command('test_report.xml', testProg,
	"./a.out --gtest_output=xml:${TARGET}")
coverageReport = testEnv.Command('coverage.xml', testReport,
	"gcovr -x -r build -o ${TARGET}")

Default(coverageReport)
