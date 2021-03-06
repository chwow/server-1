# Copyright (C) 2005-2011 MaNGOS <http://getmangos.com/>
# Copyright (C) 2009-2011 MaNGOSZero <https://github.com/mangos-zero>
#
# This program is free software; you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation; either version 2 of the License, or
# (at your option) any later version.
#
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with this program; if not, write to the Free Software
# Foundation, Inc., 59 Temple Place, Suite 330, Boston, MA  02111-1307  USA

file(GLOB_RECURSE framework_SRCS RELATIVE ${CMAKE_CURRENT_SOURCE_DIR} *.cpp *.h)

source_group("Other"            REGULAR_EXPRESSION .*)
source_group("GameSystem"       REGULAR_EXPRESSION GameSystem)
source_group("Platform"         REGULAR_EXPRESSION Platform)
source_group("Policies"         REGULAR_EXPRESSION Policies)
source_group("Utilities"        REGULAR_EXPRESSION Utilities)
source_group("LinkedReference"  REGULAR_EXPRESSION LinkedReference)
source_group("Dynamic"          REGULAR_EXPRESSION Dynamic)

include_directories(
  "${CMAKE_CURRENT_SOURCE_DIR}"
  "${ACE_INCLUDE_DIR}"
  "${TBBMalloc_INCLUDE_DIR}")

add_library(framework STATIC ${framework_SRCS})

if(NOT USE_STD_MALLOC)
  if(NOT TBB_USE_EXTERNAL)
    add_dependencies(framework tbbmalloc)
  endif()
  target_link_libraries(framework "${TBBMalloc_LIBRARY}")
endif()

if(NOT ACE_USE_EXTERNAL)
  add_dependencies(framework ace)
endif()
